<script setup lang="ts">
import InputFormatadorExcell from "./InputFormatadorExcel.vue"
import {ref} from "vue";

const valorInput = ref<Number|null>(null)
</script>

<template>
  <div id="app-bloco">
    {{valorInput}}<br><br>
    <InputFormatadorExcell
      v-model="valorInput"
    />

    <button @click="valorInput = null">clear</button>
  </div>
</template>

<style>
#app-bloco {
}
</style>