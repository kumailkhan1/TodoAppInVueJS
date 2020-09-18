<template>
<div class="todo-item" :class='{"is-complete":todo.completed}'>
    <p>
        <input type="checkbox" @change="markAsComplete">
        
        {{todo.title}}</p>
</div>
    
</template>

<script>
export default {
    name:"TodoItem",
    props:["todo"],
    methods:{
        markAsComplete : function(){
             this.todo.completed = !this.todo.completed;
        }
    }
}
</script>


<style scoped>
  .todo-item {
    background: #f3ecc2;
    padding: 10px;
    border-bottom: 1px #ccc dotted;
  }
  .is-complete {
    text-decoration: line-through;
  }
  .del {
    background: #ff0000;
    color: #fff;
    border: none;
    padding: 5px 9px;
    border-radius: 50%;
    cursor: pointer;
    float: right;
  }

</style>