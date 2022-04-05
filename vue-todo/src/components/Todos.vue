<template>
  <div v-if="todos.length > 0">
    <div>
      <TodoItem
        :key="todo.id"
        v-for="(todo, i) in todos"
        :index="i"
        :id="todo.id"
        :title="todo.title"
        :todo="todo"
        v-on:del-todo="$emit('del-todo', todo.id)"
        :todos="todos"
      />
    </div>
    <h3 class="count__app">
      Count: <b>{{ updateCount }}</b>
    </h3>
  </div>
  <h2 v-else class="text__no__tasks">The list is empty.</h2>
</template>

<script>
import TodoItem from "./TodoItem.vue";
export default {
  name: "Todos-app",
  components: {
    TodoItem,
  },
  props: ["todos"],
  computed: {
    updateCount() {
      return this.todos.length;
    },
  },
};
</script>

<style scoped>
.text__no__tasks {
  text-align: center;
  color: #ffffff;
  margin: 50px 0 0 0;
  text-decoration: underline #ff6413;
}
.count__app {
  color: white;
  margin-top: 10px;
  font-weight: 200;
  font-size: 20px;
}
</style>
