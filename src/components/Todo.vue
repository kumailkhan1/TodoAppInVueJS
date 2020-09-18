<template>
  <div>
      <div v-for="todo in todos" :key="todo.id">
         <TodoItem v-bind:todo="todo"/>
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
  }
};
</script>

<style scoped>
</style>