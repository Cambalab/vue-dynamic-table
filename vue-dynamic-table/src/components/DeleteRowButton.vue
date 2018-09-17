<template lang="html">
  <div class="">
    <i v-if="this.showMinusButton"
      :class="this.typeButtonClass"
      v-on:click="deleteRow()"
      data-toggle="tooltip"
      :data-original-title="this.tooltipTitle">
    </i>
  </div>
</template>

<script>
export default {
  props: {
    showMinusButton: {
      type: Boolean,
      required: false,
      default: false
    },
    typeButtonClass: {
      type: String,
      required: false,
      default: 'fa fa-trash-o x2'
    },
    tooltipTitle: {
      type: String,
      required: false,
      default: 'Delete'
    }
  },
  methods: {
    deleteRow() {
      this.$emit('deleteRow')
    }
  }
}
</script>

<style lang="css">
</style>
