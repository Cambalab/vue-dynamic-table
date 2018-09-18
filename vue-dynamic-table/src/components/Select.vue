<template lang="html">
  <select class="form-control" v-model="selectedOption" @change="selectOption(selectedOption)">
    <option v-bind:value="null">{{this.placeholder}}</option>
    <option v-for="option in OptionsList" class="item-text" v-bind:value="option.id">{{option.text}}</option>
  </select>
</template>
<script>
export default {

  name: 'select',
  data() {
    return {
      selectedOption: null
    }
  },
  props: {
    OptionsList: {
      type: Array,
      required: true
    },
    selected: {
      type: Number
    },
    index: {
      type: Number
    },
    placeholder: {
      type: String,
      required: false,
      default: 'Select an option'
    },
    data: {
      type: Number,
      required: false
    }
  },
  watch: {
    selected: function(newVal, oldVal) {
      this.selectedOption = newVal
    },
    data: function(newVal, oldVal) {
      this.selectOption(this.data)
    }
  },
  methods: {
    selectOption(currentOption) {
      this.$emit('selectOption', { selectedOption: currentOption, index: this.index })
    },
    refreshData() {
      if (this.data) {
        this.selectedOption = this.data
      }
    }
  },
  created() {
    this.refreshData()
  }
}
</script>
<style lang="css">
select{
  cursor: pointer;
}
</style>
