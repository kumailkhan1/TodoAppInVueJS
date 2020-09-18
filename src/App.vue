<template>
  <div id="app">
    <Header />
    <div>
      <Todo v-bind:todos="todos" />
    </div>
  </div>
</template>

<script>
import Header from "./components/layout/Header";
import Todo from "./components/Todo";

export default {
  name: "App",
  components: {
    Header,
    Todo,
  },
  data() {
    return {
      todos: [
        {
        id:1,
        title:"Hello World",
        completed:true
      },
      {
        id:2,
        title:"Hello World 2",
        completed:false
      }
      ],
    };
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
