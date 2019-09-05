<template>
  <div>
    /* main input */
    <input type="text" :value="input" @keyup="update" placeholder="검색어를 입력해주세요."/>
    /* suggest list render here */
    <div v-for="({id, name}) in tempInputList" :key="id">{{name}}</div>
  </div>
</template>

<script>
import uuidv4 from 'uuid/v4'
import { _ } from 'vue-underscore'
export default {
  name: 'input-autocomplete',
  data() {
    return {
      input: ''
    }
  },
  computed: {
    tempInputList() {
      // ex : sugeest api response Array here
      return this.input.split('').map(str => ({ id: uuidv4(), name: str }))
    }
  },
  methods: {
    update: _.throttle(function(e) {
      this.input = e.target.value
      // call suggest api here
    }, 300)
  }
}
</script>
