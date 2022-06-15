<template>
  <form @submit="addItem">
    <input type="text" placeholder="thêm công việc mới ....." v-model="title"  >
    <input type="submit" value="thêm" class="btn btn-primary">
  </form>
</template>

<script>
import {ref} from 'vue';
import {v4 as uuidv4} from 'uuid'
export default {
name:'my-AddTodo',
setup(props,context){
    const title=ref('')
  const addItem=(e)=>{
e.preventDefault();
const newItem={
    id:uuidv4(),
    title:title.value,
    completed:false
}
context.emit('add-todo',newItem)
title.value=''
  }
    return{
        title,addItem
    }
}
}
</script>

<style scoped>
form {
    display: flex;
    
}
input[type='text']{
    flex: 10;
    padding: 0,4rem;
}
input[type='submit']{
    flex: 2;
    padding: 0,4rem;
}
</style>