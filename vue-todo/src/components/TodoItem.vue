<template>
  <div class="container__todo__app">
    <div class="container__item__app" :class="{ done: isTodoCompleted }">
      <div class="block__input__app">
        <span class="text__item__app"
          ><b class="index__count">{{ index + 1 }}.</b
          >{{ toUpperCase(todo.title) }}</span
        >
      </div>
      <div class="block__button__app">
        <button
          class="button__todo__app btn"
          v-on:click="doneTask"
          :checked="todo.completed"
        >
          Check
        </button>
        <button class="button__todo__app btn" @click="updateTodo">Edit</button>
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
          <button class="button__todo__app btn__item">Save</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todos", "title", "id", "todo", "index"],
  methods: {
    toUpperCase(title) {
      return title.toUpperCase();
    },
    doneTask() {
      console.log("doneTask");
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
  computed: {
    isTodoCompleted() {
      return this.completed;
    },
  },
  data() {
    return {
      flag: false,
      updateTitle: "",
      completed: false,
    };
  },
};
</script>

<style scoped>
.container__item__app {
  background: #ffffff11;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 5px;
  width: 600px;
  margin-top: 20px;
  border: 1px solid #ff6413;
}
.done {
  text-decoration: line-through;
}
.index__count {
  color: #ff6413;
  margin-right: 5px;
}
.input__check__app {
  margin: 10px;
}
.text__item__app {
  font-size: 17px;
  word-break: break-all;
  color: white;
}
.button__todo__app {
  padding: 5px 10px;
  background-color: #ff6413;
  color: #fff;
  border: none;
}
.button__todo__app:hover {
  cursor: pointer;
  background-color: #ff7b34;
  transform: 0.3s;
}
.btn {
  margin-right: 5px;
}
.btn__item {
  margin: 0 0 0 5px;
}
.input__item__app {
  margin-top: 5px;
  width: 400px;
  padding: 8px 5px 0 5px;
  outline: none;
  border: none;
  border-bottom: 3px solid #ff6413;
}
</style>
