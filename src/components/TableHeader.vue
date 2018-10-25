<template lang="html">
  <div class="flex-row-container">
    <div v-for="column in this.columnsHeader" :key="column.name" class="flex-tableHeader">
      <label class="header-text">{{ replaceUnderscores(column.name) }}</label>
    </div>
    <AddRowButton v-if="this.showAddRowButton" v-on:addNewRow="addNewRow()"></AddRowButton>
  </div>
</template>

<script>

import AddRowButton from './AddRowButton.vue'
export default {
  name: 'TableHeader',
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
    addNewRow () {
      this.$emit('addNewRow')
    },
    replaceUnderscores (text) {
      return text.replace(/[_-]/g, ' ')
    }
  },
  created () {
  }
}
</script>

<style scoped>

</style>
