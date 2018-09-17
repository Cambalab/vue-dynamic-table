<template>
  <div class="flex-buttons-container" style="width: 100%">
    <button type="button" class="btn btn-outline-light margin3">1 Row Table</button>
    <button type="button" class="btn btn-outline-light margin3">2 Row Table</button>
    <button type="button" class="btn btn-outline-light margin3">3 Row Table</button>
    <button type="button" class="btn btn-outline-light margin3">4 Row Table</button>
    <button type="button" class="btn btn-outline-light margin3">5 Row Table</button>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .margin3 {
    margin: 3px 3px 3px 3px;
  }
  .flex-buttons-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: calc(100%/5);
    .font-style {
      font-family: 'Avenir', Helvetica, Arial, sans-serif;
      -webkit-font-smoothing: antialiased;
      -moz-osx-font-smoothing: grayscale;
      text-align: center;
      color: #2c3e50;
    }
  }
</style>
