<template>
  <div id="app">
    <h1>Todo App</h1>
    <AddTodo v-on:addtodo="addtodo" />
    <Todo
      v-on:deletetodo="deletetodo"
      v-on:checktodo="checktodo"
      v-for="todo of todos"
      :key="todo.id"
      :todo="todo"
    />
    <StatusBar v-if="todos.length > 0" :todos="todos" />
  </div>
</template>

<script>
import Todo from "./components/Todo.vue";
import AddTodo from "./components/AddTodo.vue";
import StatusBar from "./components/StatusBar.vue";
export default {
  name: "App",
  components: {
    Todo,
    AddTodo,
    StatusBar,
  },
  methods: {
    addtodo(todo) {
      this.todos = [
        ...this.todos,
        { id: Math.random() * 255, text: todo, done: false },
      ];
      //console.log(todo);
    },
    checktodo(id) {
      console.log(id);
      this.todos.forEach((todo) => {
        if (todo.id === id) {
          return (todo.done = !todo.done);
        }
      });
    },
    deletetodo(id) {
      this.todos = this.todos.filter((i) => i.id != id);
    },
  },
  data() {
    return {
      todos: [
        { id: 1, text: "Todo one", done: false },
        { id: 2, text: "Todo two", done: true },
      ],
    };
  },
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
h1 {
  margin-bottom: 50px;
}
</style>
