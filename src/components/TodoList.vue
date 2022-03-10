<template>
  <div class="outer">
    当前记录条数: {{counts}}
    <input class="input" v-model="title" @keydown.enter="add" />
    <ul class="list">
      <li v-for="item in todoList" :key="item.title">
        <input type="checkbox" v-model="item.done"  />
        {{item.title}}
      </li>
    </ul>
    <div>
      <input type="checkbox" v-model="allDone" />
      全选 {{ active }} / {{ counts }}
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref, computed } from "vue"
function useTodo(){
  let title = ref('')
  const todoList = ref([{title: 'vue', done: false}])
  function add() {
    if(title.value === ''){
      return
    }
    todoList.value.push({
      title: title.value,
      done: false
    })
    title.value = ''
  }
  const counts = computed(() => todoList.value.length)
  const active = computed(() => todoList.value.filter((item: any) => !item.done).length)
  const allDone = computed({
    get: () => active.value === 0,
    set: (value) => {
      todoList.value.forEach((todo) => { todo.done = value; });
    }
  })
  return {title, todoList, add, counts, active, allDone}
}
const  {title, todoList, add, counts, active, allDone} = useTodo()

</script>

<style scoped>
.outer {
  position: relative;
  width: 250px;
}
.input{
  height: 30px;
  line-height: 30px;
  width: 100%;
  border-radius: 3px;
  border: 1px solid #ddd;
  box-sizing: border-box;
  padding: 10px;
}
</style>
