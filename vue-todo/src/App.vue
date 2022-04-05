<template>
  <div class="main__app">
    <AddTodo v-on:add-todo="addTodo" />
    <Todos :todos="todos" 
    v-on:del-todo="deleteTodo" 
    />
  </div>
</template>

<script>
import Todos from "./components/Todos";
import AddTodo from "./components/AddTodo";
export default {
  name: "App",
  data() {
    return {
      todos: [],
    };
  },
  components: {
    Todos,
    AddTodo,
  },
  mounted() {
    const data = localStorage.getItem("tasks");
    if (data) {
      this.todos = JSON.parse(data);
    }
  },
  methods: {
    addTodo(newTodo) {
      this.todos.push(newTodo);
      this.title = "";
      localStorage.setItem("tasks", JSON.stringify(this.todos));
    },
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
      localStorage.setItem("tasks", JSON.stringify(this.todos));
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: sans-serif;
}
.main__app {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 10px;
  width: 700px;
}
</style>
