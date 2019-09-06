<template>
  <div class="comp_example">
    <SearchBar @emitRequestSearch="requestSearch"></SearchBar>
    <div class="result">{{searchResult}}</div>
  </div>
</template>

<script>
import SearchBar from './SearchBar'
export default {
  name: 'comp_example',
  components: {
    SearchBar
  },
  data() {
    return {
      searchResult: null
    }
  },
  computed: {
    hasSearchResult() {
      return !!this.searchResult
    }
  },
  methods: {
    requestSearch(input) {
      // 검색 결과 api 요청 후 결과를 searchResult 에 담는다
      console.log('requestSearch', input)
      this.searchResult = `검색결과 랜딩 : ${input}`
    }
  }
}
</script>

<style scoped>
.comp_example{
  padding:50px;
  background-color:green
}
.comp_example .result {
  height: 300px;
  margin-top: 10px;
  font-size: 20px;
  background-color: black;
  color: #fff;
}
</style>