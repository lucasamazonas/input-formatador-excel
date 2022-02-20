<script lang="ts" setup>
import {computed, ref} from "vue";

interface Props {
  modelValue?: Number
}
const {modelValue} = defineProps<Props>()

const focadoNoInput = ref<Boolean>(false)

const emit = defineEmits<{
  (e: 'update:modelValue', value: Number|null): void
}>()

const valorVisivel = computed(() => {
  if (focadoNoInput.value) {
    return modelValue
  }
  return adicionaMascara(modelValue);
})

const atualizarValor = (novoValor?: String) => {
  if (focadoNoInput.value) {
    emit('update:modelValue', Number(novoValor))
  } else {
    const valorStr = novoValor ? `${novoValor}` : ''
    emit('update:modelValue', removeMascara(valorStr))
  }
}

const removeMascara = (valorStr: String): Number => {
  const novoValor = valorStr
      .replace(".", "")
      .replace(",", ".")
      .trim()

  return Number(novoValor)
}

const adicionaMascara = (valor?: Number): String => {
  if (!valor) {
    return ''
  }
  return new Intl.NumberFormat().format(Number(valor))
}
</script>

<template>
  {{modelValue}}<br>
  <input
      :value="valorVisivel"
      v-on:input="atualizarValor($event.target.value)"
      @focus="focadoNoInput = true"
      @blur="focadoNoInput = false"
  />
</template>

<style scoped>

</style>