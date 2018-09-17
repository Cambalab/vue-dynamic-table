<template lang="html">
  <label>
    <input
      class="form-control"
      :type="this.type"
      :placeholder="this.placeholder"
      :disabled="this.disabled"
      v-model="textInputValue"
      @change="newTextInputValue(textInputValue)">
  </label>
</template>
<script>
export default {
  name: 'textInput',
  data() {
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
      default: 'Add some description...'
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
    fetchedValue: {
      type: String,
      required: false
    }
  },
  methods: {
    newTextInputValue(newValue) {
      this.$emit('newTextInputValue', { textInputValue: newValue, index: this.index })
    },
    refreshDatos() {
      if (this.fetchedValue) {
        this.textInputValue = this.fetchedValue
      }
    }
  },
  watch: {
    textValue: function(newVal, oldVal) {
      this.textInputValue = newVal
    },
    fetchedValue: function(newVal, oldVal) {
      this.textInputValue = newVal
    }
  },
  created() {
    this.refreshDatos()
  }
}
</script>
<style lang="css">
.form-control:hover{
  border: 1px solid #3c8dbc;
}
</style>
