<template>
  <div>
      <div v-for="todo in todos" :key="todo.id">
         <TodoItem 
         v-bind:todo="todo" 
         v-on:del-todo="$emit('del-todo',todo.id)" 
         v-on:change-edit-status="$emit('change-edit-status',todo.id)"
         v-on:edit-todo="$emit('edit-todo',todo.id,todo.title,todo.completed,todo.edit)"/>
      </div>
  </div>
</template>



<script>
import TodoItem from "./TodoItem";

export default {
  name: "Todo",
  props:["todos"],
  components:{
      TodoItem
  },
  methods:{
      
  }
};
</script>

<style scoped>
</style>