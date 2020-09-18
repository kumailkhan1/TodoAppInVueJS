<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <div>
      <Todo
        v-bind:todos="todos"
        v-on:del-todo="deleteTodo"
        v-on:change-edit-status="changeEditStatus"
        v-on:edit-todo="editTodo"
        v-on:mark-complete="markComplete"
      />
    </div>
  </div>
</template>

<script>
import Header from "./components/layout/Header";
import Todo from "./components/Todo";
import AddTodo from "./components/AddTodo";

export default {
  name: "App",
  components: {
    Header,
    Todo,
    AddTodo,
  },
  data() {
    return {
      todos: JSON.parse(localStorage.getItem("Todos")),
    };
  },
  methods: {
    deleteTodo: function (id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
      localStorage.setItem("Todos", JSON.stringify(this.todos));
    },
    changeEditStatus: function (id) {
      this.todos.forEach((todo) => {
        if (todo.id === id) {
          todo.edit = !todo.edit;
        }
        localStorage.setItem("Todos", JSON.stringify(this.todos));
      });
    },
    editTodo: function (id, title, completed, edit) {
      this.todos.forEach((todo) => {
        if (todo.id == id) {
          todo.title = title;
          todo.completed = completed;
          todo.edit = edit;
          
        }
      });
      localStorage.setItem("Todos", JSON.stringify(this.todos));
    },
    addTodo: function (newTodo) {
      if (JSON.parse(localStorage.getItem("Todos")) === null) {
        this.todos = [];
        this.todos.push(newTodo);
        localStorage.setItem("Todos", JSON.stringify(this.todos));
      } else {
        this.todos = [];
        let prevObject = JSON.parse(localStorage.getItem("Todos"));
        for (let i = 0; i < prevObject.length; i++) {
          this.todos.push(prevObject[i]);
        }
        this.todos.push(newTodo);
        this.todos.sort((a, b) => (a.date < b.date ? -1 : 1));
        localStorage.setItem("Todos", JSON.stringify(this.todos));
      }
    },
    markComplete: function(complete,id){
      this.todos.forEach((todo) => {
        if (todo.id == id) {
          todo.completed = complete;
        }
      });
       localStorage.setItem("Todos", JSON.stringify(this.todos));
    }
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  line-height: 1.6;
}
</style>
