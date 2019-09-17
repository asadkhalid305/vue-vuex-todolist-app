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
const todoLimit = `?_limit=10`;

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
    deleteTodo(id) {
      Axios.delete(`${baseUrl}/${id}`)
        .then(res => (this.todos = this.todos.filter(todo => todo.id !== id)))
        .catch(err => console.log(err));
    },
    addTodo(todo) {
      Axios.post(`${baseUrl}`, todo)
        .then(res => (this.todos = [res.data, ...this.todos]))
        .catch(err => console.log(err));
    }
  },
  created() {
    Axios.get("https://jsonplaceholder.typicode.com/todos?_limit=10")
      .then(res => (this.todos = res.data))
      .catch(err => console.log(err));
  }
};
</script>

<style scoped></style>