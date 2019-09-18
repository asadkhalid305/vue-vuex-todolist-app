<template>
  <div>
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import Axios from "axios";
import Todos from "../components/Todos";
import AddTodo from "../components/AddTodo";

const baseUrl = "https://jsonplaceholder.typicode.com/todos";
const todoLimit = `limit=10`;

export default {
  name: "home",
  components: {
    Todos,
    AddTodo
  },
  data() {
    return {
      todos: []
    };
  },

  methods: {
    addTodo(todo) {
      Axios.post(`${baseUrl}`, todo)
        .then(res => (this.todos = [res.data, ...this.todos]))
        .catch(err => console.log(err));
    },
    getTodos() {
      Axios.get(`${baseUrl}?_${todoLimit}`)
        .then(res => (this.todos = res.data))
        .catch(err => console.log(err));
    },
    deleteTodo(id) {
      Axios.delete(`${baseUrl}/${id}`)
        .then(res => (this.todos = this.todos.filter(todo => todo.id !== id)))
        .catch(err => console.log(err));
    }
  },
  created() {
    this.getTodos();
  }
};
</script>

<style scoped></style>