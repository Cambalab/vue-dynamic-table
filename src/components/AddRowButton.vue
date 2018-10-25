<template lang="html" v-if="this.showPlusButton">
  <div @click="addNewRow()">
    <i :class="[this.typeButtonClass, 'plus-button']"
       data-toggle="tooltip"
       data-placement="right"
       :title="this.tooltipTitle">
    </i>
  </div>
</template>

<script>
export default {
  name: 'AddRowButton',
  props: {
    typeButtonClass: {
      type: String,
      required: false,
      default: 'fa fa-plus-square x2'
    },
    tooltipTitle: {
      type: String,
      required: false,
      default: 'Add row'
    },
    showPlusButton: {
      type: Boolean,
      required: false,
      default: true
    }
  },
  methods: {
    addNewRow () {
      this.$emit('addNewRow')
    }
  }
}
</script>

<style lang="css">
</style>
