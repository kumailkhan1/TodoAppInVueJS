<template>
  <div class="todo-item" :class="{'is-complete':todo.completed}">
    <p>
      <span v-show="todo.edit">

          <input v-model="title" type="text" />
          <input type="submit" class="done" value="Done!" @click="editTodo" />
      </span>
      <span v-show="!todo.edit">
        <input type="checkbox" :checked="todo.completed" @change="markAsComplete" />
        {{todo.title}}
      </span>
      <button class="del" @click="$emit('del-todo',todo.id)">Delete</button>
      <button class="edit" @click="$emit('change-edit-status',todo.id)">Edit</button>
    </p>
  </div>
</template>

<script>
// import uuid from "uuid";
export default {
  name: "TodoItem",
  data() {
    return {
      title: this.todo.title
    };
  },
  props: ["todo"],
  methods: {
    markAsComplete: function () {
        
      this.todo.completed = !this.todo.completed;
      this.$emit("mark-complete",this.todo.completed,this.todo.id);
    },
    editTodo: function(){
        let newEditedTodo = {
            id:this.todo.id,
            title:this.title,
            completed:false,
            edit:false
        }
        this.todo.title = this.title;
        this.todo.completed = false;
        this.todo.edit = false;
        this.$emit('edit-todo',this.todo.id,this.todo.title,this.todo.completed,this.todo.edit);
        console.log(newEditedTodo)
        this.title="";
    },
  },
  
};
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
  background: #e8505b;
  color: #fff;
  border: none;
  padding: 5px 9px;
  cursor: pointer;
  float: right;
}

.edit {
  background: #14b1ab;
  color: #fff;
  border: none;
  padding: 5px 9px;
  margin-right: 3px;
  cursor: pointer;
  float: right;
}

.done {
  background: #f9d56e;
  color: #fff;
  border: none;
  padding: 5px 9px;
  margin-left: 3px;
  cursor: pointer;
}
form {
  display: inline;
}
</style>