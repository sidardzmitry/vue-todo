<template>
    <div class="container__todo__app">
        <br>
        <h1 class="title__todo__app">ToDo App</h1>
        <br>
        <form @submit.prevent="addTodo">
        <div class="box__todo__app">
            <input required type="text" v-model="title" placeholder="Add Title" name="title" id="" class="input__todo__app">
        </div>
        <div class="box__todo__app">
            <button class="button__todo__app">
                Add Todo
            </button>
        </div>
        </form>
    </div>
</template>
<script>
export default {
  name: "AddTodo",
  data() {
    return {
      title: ''
    }
  },
  methods: {
    addTodo() {
      const newTodo = {
        id:Date.now(),
        title: this.title,
        completed: false
      }
      this.$emit('add-todo', newTodo);
      this.title = '';
    }
  }
}
</script>

<style scoped>
.container__todo__app{
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
.title__todo__app{
  color: rgb(112, 9, 209);
  font-size: 55px;
}
.box__todo__app{
  padding: 10px;
  display: flex;
  justify-content: center;
}
.input__todo__app{
  width: 400px;
  padding: 10px;
}
.input__todo__app::placeholder{
  font-size: 20px;
}
.button__todo__app{
  padding: 10px 15px;
  background-color: #ff6413;
  color: #fff;
  border: none;
  align-items: center;
}
.button__todo__app:hover{
  cursor: pointer;
  background-color: #ff7b34;
  transform: 0.3s;
}
</style>