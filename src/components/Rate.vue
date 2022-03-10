<template>
  <div :style="fontStyle">
    <span v-for="num in 5" :key="num" @click="handleUpdate(num)" @mouseenter="handleMouseEnter(num)" @mouseout="handleMouseOut">
      {{num <= rate ? '★' : '☆'}}
    </span>
  </div>
</template>

<script lang="ts" setup>
import {ref, defineProps, computed, defineEmits} from 'vue'
type Theme = 'green' | 'red' | 'black'
const props = defineProps<{
  value: number,
  theme: Theme
}>()

const rate = ref(props.value)
const themeObj = {
  green: 'green',
  red: 'red',
  black: 'black'
}
const fontStyle = computed(() =>`color: ${themeObj[props.theme]}`)
const handleMouseEnter = (num: number) => {
  rate.value = num
}
const handleMouseOut = () => {
  rate.value = props.value
}
let emits = defineEmits(['update:modelValue'])
const handleUpdate = (num: number) => {
  emits('update:modelValue', num)
}
</script>