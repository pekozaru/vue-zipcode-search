<template>
  <div class="wrapper">
      <div class="container">
          <AppTitle />
          <SearchForm @submit-form="searchZipcode" />
          <SearchResults :results="results" v-if="!loading" />
          <LoadingIndicator v-if="loading" />
      </div>
  </div>
</template>

<script setup>
import { reactive, ref } from "vue"
import axios from "axios"
import AppTitle from "./components/AppTitle.vue"
import SearchForm from "./components/SearchForm.vue"
import SearchResults from "./components/SearchResults.vue"
import LoadingIndicator from "./components/LoadingIndicator.vue"
import "./assets/style.css"

const loading = ref(false)

const results = reactive({
  address1: "",
  address2: "",
  address3: ""
})

const searchZipcode = (zipcode) => {
  loading.value = true
  axios.get(`https://zipcloud.ibsnet.co.jp/api/search?zipcode=${zipcode}`)
       .then(res => {
          if (res.data.results) {
              results.address1 = res.data.results[0].address1
              results.address2 = res.data.results[0].address2
              results.address3 = res.data.results[0].address3
          } else {
              alert("該当する住所が見つかりません。")
          }
          loading.value = false
       })
       .catch(err => {
          alert("エラーが発生しました。ページをリロードして、もう一度トライしてください。")
          loading.value = false
       })
}
</script>
