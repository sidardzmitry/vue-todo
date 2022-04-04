<template>
  <div v-if="todos.length > 0">
    <div>
      <TodoItem 
      v-bind:key="todo.id"
      v-for="(todo, i) in todos" 
      v-bind:index='i'
      v-bind:id="todo.id" 
      v-bind:title="todo.title"
      v-bind:todo="todo" 
      v-on:del-todo="$emit('del-todo', todo.id)"
      v-bind:todos="todos"/>
    </div>
  </div>
  <h2 v-else class="text__no__tasks">Список пуск</h2>
  <hr>
</template>

<script>
import TodoItem from './TodoItem.vue';
export default {
  name: "Todos-app",
  components: {
    TodoItem
  },
  props: ["todos"]
}
</script>

<style scoped>
.text__no__tasks{
  text-align: center;
  color: brown;
  margin-top: 10px;
}
</style>