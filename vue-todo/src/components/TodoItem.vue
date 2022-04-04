<template>
  <div class="container__todo__app" 
  >
    <div
      class="container__item__app"
      v-bind:class="{ 'done': todo.completed }"
      >
      <div class="block__input__app">
        <input
          type="checkbox"
          v-on:change="doneTask"
          v-bind:checked="todo.completed"
          class="input__check__app"
        />
        <span class="text__item__app"><strong><b>{{index + 1}}</b>. Name:</strong>{{ toUpperCase(todo.title) }}</span>
      </div>
      <div class='block__button__app'>
        <button class="button__todo__app btn" @click="updateTodo">Update</button>
        <button @click="$emit('del-todo', todo.id)" class="button__todo__app">
          Delete
        </button>
      </div>
    </div>
    <div v-if="this.flag" class="block__update__app">
      <form @submit.prevent="updateTodoMethod">
        <div class="block__input__app">
          <input
            class="input__item__app"
            v-model="updateTitle"
            type="text"
            :placeholder="title"
            required
            
          />
        </div>
        <div class="block__button__app">
          <button class="button__todo__app">Update</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todos", "title", "id", "todo", 'index'],
  methods: {
    toUpperCase(title) {
      return title.toUpperCase();
    },
    doneTask() {
      this.completed = !this.completed;
      localStorage.setItem("tasks", JSON.stringify(this.todos));
    },
    updateTodo() {
      this.flag = !this.flag;
    },
    updateTodoMethod() {
      console.log(this.title);
      console.log(this.id);
      this.todos.filter((todo) => {
        if (todo.id == this.id) {
          todo.title = this.updateTitle;
        }
      });
      localStorage.setItem("tasks", JSON.stringify(this.todos));
      this.flag = false;
    },
  },
  data() {
    return {
      flag: false,
      updateTitle: "",
    };
  },
};
</script>

<style scoped>
.container__todo__app {}
.container__item__app {
  background: #f4f4f4;
  padding: 10px;
  margin: 10px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.done {
  text-decoration: line-through;
}
.input__check__app{
  margin: 10px;
}
.text__item__app{
  font-size: 17px;
}
.button__todo__app {
  padding: 10px 15px;
  background-color: #ff6413;
  color: #fff;
  border: none;
  align-items: center;
}
.button__todo__app:hover {
  cursor: pointer;
  background-color: #ff7b34;
  transform: 0.3s;
}
.btn{
  margin-right: 5px;
}
.block__update__app{
  padding: 10px;
}
.input__item__app{
  width: 300px;
  padding: 5px;
}
.block__input__app{
  padding: 5px;
}
</style>
