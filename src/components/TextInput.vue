<template lang="html">
  <div class="">
    <label>
      <input
        class="form-control"
        :type="this.type"
        :placeholder="this.placeholder"
        :disabled="this.disabled"
        v-model="textInputValue"
        @change="newTextInputValue(textInputValue)">
    </label>
  </div>
</template>
<script>
export default {
  name: 'TextInput',
  data () {
    return {
      textInputValue: null
    }
  },
  props: {
    textValue: {
      type: String
    },
    index: {
      type: Number
    },
    placeholder: {
      type: String,
      required: false,
      default: 'Write here...'
    },
    disabled: {
      type: Boolean,
      required: false,
      default: false
    },
    type: {
      type: String,
      required: false,
      deafult: 'text'
    },
    data: {
      type: String,
      required: false
    }
  },
  methods: {
    newTextInputValue (newValue) {
      this.$emit('newTextInputValue', { textInputValue: newValue, index: this.index })
    },
    refreshData () {
      if (this.data) {
        this.textInputValue = this.data
      }
    }
  },
  watch: {
    textValue: function (newVal, oldVal) {
      this.textInputValue = newVal
    },
    newTextInputValue: function (newVal, oldVal) {
      this.textValue = newVal
    }
  },
  created () {
    this.refreshData()
  }
}
</script>
<style lang="css">
.form-control:hover{
  border: 1px solid #3c8dbc;
}
</style>
