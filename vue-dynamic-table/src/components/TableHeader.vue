<template lang="html">
  <div class="" v-for="column in this.columnsHeader">
    <div class="">
      <label>{{ replaceUnderscores(column.text) }}</label>
    </div>
  </div>
  <AddRowButton v-if="this.showAddRowButton" v-on:addNewRow="addNewRow()"></AddRowButton>
</template>

<script>

import AddRowButton from './AddRowButton.vue'
export default {
  props: {
    columnsHeader: {
      type: Array,
      requiered: true
    },
    showAddRowButton: {
      type: Boolean,
      required: false,
      default: true
    }
  },
  components: {
    AddRowButton
  },
  methods: {
    addNewRow() {
      this.$emit('addNewRow')
    },
    replaceUnderscores(text) {
      return text.replace(/[_-]/g, ' ')
    }
  }
}
</script>

<style lang="css">
</style>
