<template lang="html">
  <div class="flex-container">
    <select class="form-control" v-model="selectedOption" @change="selectOption(selectedOption)">
      <option v-bind:value="null">{{this.placeholder}}</option>
      <option v-for="option in optionsList" class="item-text" v-bind:value="option.id" :key="option.id">{{option.text}}</option>
    </select>
  </div>
</template>
<script>
export default {

  name: 'Select',
  data () {
    return {
      selectedOption: null
    }
  },
  props: {
    optionsList: {
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
    selected: function (newVal, oldVal) {
      this.selectedOption = newVal
    },
    selectOption: function (newVal, oldVal) {
      this.selected = newVal
    }
  },
  methods: {
    selectOption (currentOption) {
      this.$emit('selectOption', { selectedOption: currentOption, index: this.index })
    },
    refreshData () {
      if (this.data) {
        this.selectedOption = this.data
      }
    }
  },
  created () {
    this.refreshData()
  }
}
</script>
<style scoped>
select{
  cursor: pointer;
}
</style>
