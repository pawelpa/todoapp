<template>
  <div id="app">
    <h1>Todo App v1.0</h1>
    <AddTodo v-on:addtodo="addtodo" />
    <Todo v-on:deletetodo="deletetodo" v-for="todo of todos" :key="todo.id" :todo="todo" />
  </div>
</template>

<script>
import Todo from "./components/Todo.vue";
import AddTodo from "./components/AddTodo.vue";
export default {
  name: "App",
  components: {
    Todo,
    AddTodo
  },
  methods: {
    addtodo(todo) {
      this.todos = [
        ...this.todos,
        { id: Math.random() * 255, text: todo, done: false }
      ];
      console.log(todo);
    },
    deletetodo(id) {
      this.todos = this.todos.filter(i => i.id != id);
    }
  },
  data() {
    return {
      todos: [
        { id: 1, text: "Todo one", done: false },
        { id: 2, text: "Todo two", done: true }
      ]
    };
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
