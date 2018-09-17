<template lang="html">
  <div class="" v-for="column in this.columnsHeader">
    <div class="">
      <label>{{ replaceUnderscores(column.text) }}</label>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    columnsHeader: {
      type: Array,
      requiered: true
    }
  },
  methods: {
    replaceUnderscores(text) {
      return text.replace(/[_-]/g, ' ')
    }
  }
}
</script>

<style lang="css">
</style>
