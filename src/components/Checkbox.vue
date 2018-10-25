<template lang="html">
  <label class="container-check">
        <input
        :class="[this.type]"
        :type="this.type"
        v-model="currentCheckboxValue"
        @change="newCheckboxValue(currentCheckboxValue)">
      <span :class="[this.type]"></span>
      <span class="check-text">
        {{ this.text }}
      </span>
  </label>
</template>

<script>
export default {
  name: 'Checkbox',
  data () {
    return {
      currentCheckboxValue: false
    }
  },
  props: {
    text: {
      type: String,
      required: false,
      default: 'aaaaaaaa'
    },
    type: {
      type: String,
      required: false,
      default: 'checkbox'
    },
    data: {
      type: Array,
      required: false
    },
    index: {
      type: Number,
      requiered: false
    }
  },
  methods: {
    newCheckboxValue (newValue) {
      this.$emit('newCheckboxValue', {checkboxValue: newValue})
    },
    refreshData () {
      if (this.data.includes(this.index + 1)) {
        this.currentCheckboxValue = true
      } else {
        if (this.data.includes(true)) {
          this.currentCheckboxValue = true
        }
      }
    }
  },
  watch: {
    checked: function (newVal, oldVal) {
      this.currentCheckboxValue = newVal
    },
    data: function () {
      if (this.data) {
        if (this.data.includes(this.index + 1)) {
          this.currentCheckboxValue = true
        } else {
          if (this.data.includes(true)) {
            this.currentCheckboxValue = true
          }
        }
      }
    }
  },
  created () {
    if (this.data) {
      this.refreshData()
    }
  }
}
</script>
<style scoped>

</style>
