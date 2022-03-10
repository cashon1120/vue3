<template>
  <transition name="fade">
    <h1 v-if="showTitle">{{ x }}</h1>
  </transition>
  <TodoList />
  <Rate v-model:value="rate1" theme="green"/>
  <Rate v-model:value="rate2" theme="red" />
  <Rate v-model:value="rate3" theme="black" />
  <button @click="toggleShow">click</button>
</template>

<script setup>
import { ref, computed } from "vue"
import TodoList from "../components/TodoList.vue"
import Rate from "../components/Rate.vue"
import useMouse from "../utils/mouse"

const { x, y } = useMouse()
const color = computed(() => (x.value > 100 ? "red" : "black"))

const rate1 = ref(1)
const rate2 = ref(2)
const rate3 = ref(3)

const handleUpdateRate1 = (newValue) => {
    rate1.value = newValue
}

const showTitle = ref(true)
const toggleShow = () => {
  showTitle.value = !showTitle.value
}
defineExpose({
    rate1,
    rate2,
    rate3,
    color
})
</script>

<style>
h1 {
  color: v-bind(color);
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s linear;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
