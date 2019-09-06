<template>
  <div id="app">
    <ExamplePage></ExamplePage>
  </div>
</template>

<script>
import ExamplePage from './components/ExamplePage.vue'

export default {
  name: 'app',
  components: {
    ExamplePage
  }
}
</script>

<style>
*{margin:0;padding:0}
body{background-color:seashell}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 60px auto;
  width:600px;
}
</style>
