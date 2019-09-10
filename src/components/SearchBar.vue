<template>
  <div class="comp_search_bar">
    <div class="search_box">
      <input
        v-model="input"
        @keyup="onChangeUpdate"
        @focus="onChangeUpdate"
        @blur="onBlurSuggest"
        type="text"
        class="inp_search"
        placeholder="검색어를 입력해주세요."
      />
    </div>

    <div v-if="isOpenSuggest" class="suggest_box">
      <button
        v-for="({id, name}) in suggestList"
        :key="id"
        @click="onClickSearch(name)"
        @focus="openSuggest"
        @blur="onBlurSuggest"
        class="item_suggest"
      >{{name}}</button>
    </div>

    <button type="button" class="btn_search" @click="emitRequestSearch">검색</button>
  </div>
</template>

<script>
import uuidv4 from 'uuid/v4'
import { _ } from 'vue-underscore'
// emit events 부모 컴포넌트에게 요청
const EMIT_REQUEST_SEARCH = 'emitRequestSearch' // 검색 결과 api 요청 이벤트 명
const WAITING_TIME = 0
export default {
  name: 'search-bar',
  data() {
    return {
      input: '',
      suggestList: [],
      isOpenSuggest: false
    }
  },
  computed: {
    hasSuggestList() {
      return this.suggestList.length > 0
    }
  },
  methods: {
    onChangeUpdate: _.throttle(function(evt) {
      this.input = evt.target.value
      evt.keyCode === 13 ? this.emitRequestSearch() : this.requestSuggest()
    }, WAITING_TIME),
    onClickSearch(selectedWord) {
      this.input = selectedWord
      this.emitRequestSearch()
    },
    onBlurSuggest(evt) {
      if (!evt.relatedTarget) return this.closeSuggest()
      if (!evt.relatedTarget.className) return this.closeSuggest()
      if (evt.relatedTarget.className !== 'item_suggest') return this.closeSuggest()
    },
    resetSuggestList() {
      this.suggestList = []
    },
    openSuggest() {
      if (!this.hasSuggestList) return
      this.isOpenSuggest = true
    },
    closeSuggest() {
      this.isOpenSuggest = false
    },
    requestSuggest() {
      // FIXME: temp call seggest api
      this.suggestList = this.input.split('').map(str => ({ id: uuidv4(), name: str }))
      this.openSuggest()
    },
    emitRequestSearch() {
      console.table({
        name: EMIT_REQUEST_SEARCH,
        param: this.input
      })
      this.$emit(EMIT_REQUEST_SEARCH, this.input)
      this.resetSuggestList()
    }
  }
}
</script>

<style scoped>
.comp_search_bar {
  position: relative;
  background-color: #fff;
  z-index: 10;
}
.comp_search_bar .search_box {
  overflow: hidden;
  padding-right: 50px;
  border: 1px solid #959595;
}
.comp_search_bar .inp_search {
  float: left;
  width: 100%;
  height: 30px;
  text-indent: 10px;
  border: 0 none;
}
.comp_search_bar .btn_search {
  position: absolute;
  top: 0;
  right: 0;
  width: 50px;
  height: 100%;
  background-color: #efefef;
}
.comp_search_bar .suggest_box {
  overflow-y: scroll;
  overflow-x: auto;
  position: absolute;
  top: 32px;
  left: 0;
  right: 0;
  max-height: 240px;
  background-color: #fff;
  border: 1px solid #959595;
}
.comp_search_bar .item_suggest {
  display: inline-block;
  width: 100%;
  height: 24px;
  text-align: left;
  text-indent: 10px;
  border: 0 none;
}
.comp_search_bar .item_suggest:hover {
  background-color: #efefef;
}
.comp_search_bar .item_suggest:focus {
  background-color: #efefef;
  outline: 0;
}
</style>