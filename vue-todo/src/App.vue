<template>
  <div class="main__app">
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import Todos from './components/Todos';
import AddTodo from './components/AddTodo'
export default {
  name: 'App',
  data(){
    return {
      todos:[
        {
          id:1,
          title:"todo 1",
          completed:false
        },
      ]
    }
  },
  components: {
    Todos,
    AddTodo
  },
    mounted() {
    const data = localStorage.getItem("tasks");
    if (data) {
      this.tasks = JSON.parse(data);
    }
  },
  methods:{
    addTodo(newTodo){
      this.todos = [...this.todos,newTodo]
      localStorage.setItem("tasks", JSON.stringify(this.todos));
    },
    deleteTodo(id){
      this.todos = this.todos.filter((todo) => todo.id !== id)
      localStorage.setItem("tasks", JSON.stringify(this.todos));
    }
  }
};
</script>

<style lang="scss">
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.main__app{
  width: 700px;
  margin-left: 25%;
}
</style>
