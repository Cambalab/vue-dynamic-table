<template lang="html">

</template>

<script>
export default {
  props: {
    columns: {
      type: Array,
      required: true
    },
    rows: {
      type: Array,
      required: true
    },
    currentElement: {
      type: Object,
      required: true
    },
    index: {
      type: Number,
      required: true
    },
    showPlusButton: {
      type: Boolean,
      required: false,
      default: true
    },
    showMinusButton: {
      type: Boolean,
      required: false,
      default: true
    },
    dataBrought: {
      type: Object,
      required: false,
      default: {}
    }
  },
  components: {
  },
  computed: {
  },
  methods: {
  },
  watch: {
  },
  create() {
  }
}
</script>

<style lang="css">
</style>
