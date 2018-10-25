<template lang="html">
  <div class="flex-minus-button">
    <i v-if="this.showMinusButton"
      :class="[this.typeButtonClass, 'minus-button']"
      v-on:click="deleteRow()"
      data-toggle="tooltip"
      data-placement="right"
      :title="this.tooltipTitle">
    </i>
  </div>
</template>

<script>
export default {
  name: 'DeleteRowButton',
  props: {
    showMinusButton: {
      type: Boolean,
      required: false,
      default: true
    },
    typeButtonClass: {
      type: String,
      required: false,
      default: 'fa fa-trash x2'
    },
    tooltipTitle: {
      type: String,
      required: false,
      default: 'Delete'
    },
    index: {
      type: Number,
      required: true
    }
  },
  methods: {
    deleteRow () {
      this.$emit('deleteRow', this.index)
    }
  }
}
</script>

<style lang="css">
</style>
