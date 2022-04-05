<template>
  <div class="container__todo__app">
    <br />
    <img src="../assets/logo.svg" alt="TodoApp" />
    <br />
    <form @submit.prevent="addTodo">
      <div class="box__todo__app">
        <input
          required
          type="text"
          v-model="title"
          placeholder="Add Title"
          class="input__todo__app"
        />
      </div>
      <div class="box__todo__app">
        <button class="button__todo__app">Add Todo</button>
      </div>
    </form>
  </div>
</template>
<script>
export default {
  name: "AddTodo",
  data() {
    return {
      title: "",
    };
  },
  methods: {
    addTodo() {
      const newTodo = {
        id: Date.now(),
        title: this.title,
        completed: false,
      };
      this.$emit("add-todo", newTodo);
      this.title = "";
    },
  },
};
</script>

<style scoped>
.container__todo__app {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
.title__todo__app {
  color: #ffffff;
  font-size: 55px;
}
.box__todo__app {
  padding: 5px;
  display: flex;
  justify-content: center;
  flex-direction: column;
}
.input__todo__app {
  width: 500px;
  padding: 8px 5px 0 8px;
  outline: none;
  border: none;
  border-bottom: 3px solid #ff6413;
}
.input__todo__app::placeholder {
  font-size: 15px;
}
.button__todo__app {
  padding: 5px 10px;
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
</style>
