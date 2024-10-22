<template>
  <form @submit.prevent="submitForm">
      <input type="text" v-model="zipcode" placeholder="郵便番号を入力">
      <button type="submit">検索</button>
  </form>
</template>

<script setup>
import { ref } from "vue"

const zipcode = ref("")

const submitForm = () => {
  emits("submit-form", zipcode.value)
  zipcode.value = ""
}

const emits = defineEmits(["submit-form"])
</script>
