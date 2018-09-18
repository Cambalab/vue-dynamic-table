<template lang="html" v-if="this.showPlusButton">
  <div class="" @click="addNewRow()">
    <i  :class="this.typeButtonClass"
        data-toggle="tooltip"
        :data-original-title="this.tooltipTitle">
    </i>
  </div>
</template>

<script>
export default {
  props: {
    typeButtonClass: {
      type: String,
      required: false,
      default: 'fa fa-plus-square-o x2'
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
    addNewRow() {
      this.$emit('addNewRow')
    }
  }
}
</script>

<style lang="css">
</style>
