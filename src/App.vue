<template>
  <div id="app">
    <input-autocomplete @eventrequestSearch="requestSearch"></input-autocomplete>
  </div>
</template>

<script>
import InputAutocomplete from './components/InputAutocomplete.vue'

export default {
  name: 'app',
  components: {
    InputAutocomplete
  },
  methods:{
    requestSearch(input){
      console.log('requestSearch', input)
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
