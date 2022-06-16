<template>
<AddTodo @add-todo="addTodo" />
 <TodoItem v-for="todo in todos" :key="todo" :todoProps="todo" @item-completed="markComplete" @delete-item="deleteItem"  />

</template>

<script>
import { ref } from 'vue'
import TodoItem from './TodoItem.vue'
import AddTodo from "./AddTodo.vue"
import axios from 'axios'
// import {v4 as uuidv4} from 'uuid'
export default {
  components: { TodoItem,AddTodo },
name:"myTodos",
setup(){
    const todos=ref([]);
     const getAllTodos = async () => {
      try {
        const res = await axios.get(
          'https://jsonplaceholder.typicode.com/todos?_limit=5'
        )
        // console.log(res.data)
        todos.value = res.data
    // console.log(todos.value)

      } catch (error) {
        console.log(error)
      }
    }

    getAllTodos()
const markComplete=(id)=>{
todos.value=todos.value.map(todo=>{
  if(todo.id===id) todo.completed =! todo.completed
  return todo
})
}
const deleteItem= async (id)=>{
  try {
    await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
    todos.value=todos.value.filter(todo=>todo.id!==id)
  } catch (error) {
    console.log(error)
  }

}
const addTodo= async(newTodo)=>{
  try {
    const {data}= await axios.post('https://jsonplaceholder.typicode.com/todos',newTodo)
    todos.value.push(data)
  } catch (error) {
    console.log(error)
  }
}
    return {
        todos,
        markComplete,deleteItem,addTodo
    }
}
}
</script>

<style>

</style>