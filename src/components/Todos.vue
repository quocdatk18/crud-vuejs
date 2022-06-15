<template>
<AddTodo @add-todo="addTodo" />
 <TodoItem v-for="todo in todos" :key="todo" :todoProps="todo" @item-completed="markComplete" @delete-item="deleteItem"  />

</template>

<script>
import { ref } from 'vue'
import TodoItem from './TodoItem.vue'
import AddTodo from "./AddTodo.vue"
import {v4 as uuidv4} from 'uuid'
export default {
  components: { TodoItem,AddTodo },
name:"myTodos",
setup(){
    const todos=ref([{
      id:uuidv4(),
      title:"viec 1",
      completed:true
    },
    {
      id:uuidv4(),
      title:"viec 2",
      completed:true
    },
    {
      id:uuidv4(),
      title:"viec 3",
      completed:false
    },
    {
      id:uuidv4(),
      title:"viec 4",
      completed:true
    },
    ])
const markComplete=(id)=>{
todos.value=todos.value.map(todo=>{
  if(todo.id===id) todo .completed =! todo.completed
  return todo
})
}
const deleteItem=(id)=>{
  todos.value=todos.value.filter(todo=>todo.id!==id)
  return todos

}
const addTodo=(newTodo)=>{
  todos.value.push(newTodo)
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