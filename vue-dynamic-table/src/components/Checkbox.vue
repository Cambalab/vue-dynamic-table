<template lang="html">
  <div class="input-group mb-3">
    <div class="input-group-prepend">
      <div class="input-group-text">
        <input :type="this.type" :aria-label="this.text" v-model="currentCheckboxValue" @change="newCheckboxValue(currentCheckboxValue)">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'checkbox',
  data() {
    return {
      currentCheckboxValue: false
    }
  },
  props: {
    text: {
      type: String,
      required: false,
      default: ''
    },
    type: {
      type: String,
      required: false,
      default: 'checkbox'
    }
    fetchedValue: {
      type: Array,
      required: false
    },
    index: {
      type: Number,
      requiered: false
    }
  },
  methods: {
    newCheckboxValue(newValue) {
      this.$emit('newCheckboxValue', {checkboxValue: newValue})
    },
    refreshData() {
      if (this.fetchedValue.includes(this.index + 1)) {
        this.currentCheckboxValue = true
      } else {
        if (this.fetchedValue.includes(true)) {
          this.currentCheckboxValue = true
        }
      }
    }
  },
  watch: {
    checked: function(newVal, oldVal) {
      this.currentCheckboxValue = newVal
    },
    fetchedValue: function() {
      if (this.fetchedValue) {
        if (this.fetchedValue.includes(this.index + 1)) {
          this.currentCheckboxValue = true
        } else {
          if (this.fetchedValue.includes(true)) {
            this.currentCheckboxValue = true
          }
        }
      }
    }
  },
  created() {
    if (this.fetchedValue) {
      this.refreshData()
    }
  }
}
</script>
<style media="screen">
</style>
