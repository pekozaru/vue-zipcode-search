<template>
  <div class="address-results">
      <p v-if="address1">{{ address1 }}</p>
      <p v-if="address2">{{ address2 }}</p>
      <p v-if="address3">{{ address3 }}</p>
  </div>
</template>

<script setup>
import { toRefs } from "vue"

const props = defineProps({
  results: Object
})

const { address1, address2, address3 } = toRefs(props.results)
</script>
