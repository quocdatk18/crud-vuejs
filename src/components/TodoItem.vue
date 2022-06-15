<template>
  <p :class="['todoItem ',todoProps.completed ? 'is-completed' : '']">
    <input type="checkbox" :checked="todoProps.completed" @change="markItemCompleted" />
    {{todoProps.title}}
    <button class="btn btn-danger button" @click="deleteItem">Delete</button>
  </p>
</template>

<script>

export default {
    name:"myTodoItem",
    props:['todoProps'],
    setup(props,context){
      const markItemCompleted=()=>{
       context.emit('item-completed',props.todoProps.id)
      }
      const deleteItem=()=>{
        context.emit('delete-item',props.todoProps.id)
      }
      return {
        markItemCompleted,deleteItem
      }
    }

}
</script>

<style scoped>
.button{
  float: right;
}
.todoItem{
  background: #f4f4f4;
  padding: 0.9rem;
  margin:0 ;
  border-bottom: 1px dotted #ccc;
}
.is-completed{
text-decoration: line-through;
}
</style>