<template>
  <div>{{ count }} {{ state.foo }}, {{props.count}}</div>
  <button @click="handleClick(1)">click</button>
  <button @click="handleClick(2)">click2</button>
  <button @click="add">click3</button>
</template>

<script lang="ts">
  import { ref, reactive, defineComponent, watchEffect } from 'vue'

  export default defineComponent({
    name: 'HelloWorld',
    props: {
      count: Number,
      add: Function
    },
    setup(props, ctx) {
      const count = ref(0)
      const state = reactive({ foo: 'bar' })
      const handleClick = (type: number) => {
        if(type === 1){
          count.value++
        }else{
          state.foo = '123'
        }
      }
      const add = () => {
        ctx.emit('add')
      }
      watchEffect(() => {
        console.log(count, state, props.count)
      })
      // 暴露给模板
      return {
        count,
        state,
        add,
        handleClick,
        props
      }
    },
  })
</script>