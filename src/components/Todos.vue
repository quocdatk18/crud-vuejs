<template>
 <TodoItem v-for="todo in todos" :key="todo" :todoProps="todo" />

</template>

<script>
import { ref } from 'vue'
import TodoItem from './TodoItem.vue'
export default {
  components: { TodoItem },
name:"myTodos",
setup(){
    const todos=ref(['viec 1','viec 2','viec 3'])

    return {
        todos
    }
}
}
</script>

<style>

</style>