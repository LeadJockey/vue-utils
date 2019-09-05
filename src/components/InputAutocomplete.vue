<template>
  <div>
    <input :value="input" @keyup="updateInput" type="text" placeholder="검색어를 입력해주세요." />
    <div
      v-for="({id, name}) in tempInputList"
      :key="id"
      @click.prevent="selectInput(name)"
      class="item"
    >{{name}}</div>
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
    updateInput: _.throttle(function(e) {
      this.input = e.target.value
      e.keyCode === 13 
        ? this.emitRequestSearch() 
        : this.requestAutocompleteApi()
    }, 300),
    selectInput(name) {
      this.input = name
      this.requestAutocompleteApi()
    },
    requestAutocompleteApi() {
      console.log('requestAutocompleteApi', this.input)
    },
    emitRequestSearch() {
      console.log(
        'emitRequestSearch 부모 컴포넌트 또는 외부에서 다른 컴포넌트를 호출하는 방식 추천 : 오토컴플릿트 컴포넌트와 분리하기 위함',
        this.input
      )
      this.$emit('eventrequestSearch', this.input)
    }
  }
}
</script>

<style scoped>
.item:hover {
  background-color: #efefef;
}
</style>