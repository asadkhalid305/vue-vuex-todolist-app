<template>
  <div>
    <form @submit.prevent="addTodo">
      <input type="text" v-model="title" placeholder="Add todo..." />
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<script>
export default {
  name: "AddTodo",
  data() {
    return {
      title: ""
    };
  },

  methods: {
    addTodo() {
      const newTodo = {
        title: this.title,
        completed: false
      };

      this.$emit("add-todo", newTodo);

      this.title = "";
    }
  }
};
</script>

<style scoped>
form {
  display: flex;
}

input {
  font-size: 1em;
}

input[type="text"] {
  flex: 0.9;
  padding: 10px;
}

input[type="submit"] {
  flex: 0.1;
  background: #008cba;
  color: white;
  border: none;
  cursor: pointer;
}
</style>