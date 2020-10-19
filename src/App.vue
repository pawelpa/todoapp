<template>
  <div id="app">
    <h1>Todo App</h1>
    <AddTodo v-on:addtodo="addtodo" />
    <Todo
      v-on:deletetodo="deletetodo"
      v-on:checktodo="checktodo"
      v-for="todo of todos"
      :key="todo._id"
      :todo="todo"
    />
    <StatusBar
      v-on:all="customFilter('all')"
      v-on:left="customFilter('left')"
      v-on:done="customFilter('done')"
      :todos="todos"
      :active="active"
    />
  </div>
</template>

<script>
import Todo from "./components/Todo.vue";
import AddTodo from "./components/AddTodo.vue";
import StatusBar from "./components/StatusBar.vue";
import { v4 as uuid } from "uuid";
import PouchDB from "pouchdb";
export default {
  name: "App",
  components: {
    Todo,
    AddTodo,
    StatusBar,
  },
  methods: {
    customFilter(what) {
      switch (what) {
        case "done":
          this.todos = this.backupTodos.filter((t) => t.done === true);
          this.active = "done";
          break;
        case "all":
          if (this.backupTodos.length > this.todos.length) {
            this.todos = this.backupTodos;
          }
          this.active = "all";
          break;
        case "left":
          this.todos = this.backupTodos.filter((t) => t.done !== true);
          this.active = "left";
          break;
      }
    },
    addtodo(todo) {
      
      let _id = uuid();
      this.customFilter("all");
      this.todos = [...this.todos, { _id, text: todo, done: false }];
      this.backupTodos = this.todos;
      this.db
        .put({ _id, text: todo, done: false })
        .then(() => console.log('Todo added'))
        .catch((error) => console.log(error));
    },
    checktodo(id) {
      this.customFilter('all');
      this.todos.forEach((todo) => {
        if (todo._id === id) {
          this.db.get(`${id}`)
            .then(doc => {
              return this.db.put({ _id:id, _rev: doc._rev, text: todo.text, done: !todo.done})
            })
            .then(() => console.log('todo updated'))
            .catch((error) => console.log(error));
          return !todo.done;
        }
      });
      this.backupTodos = this.todos;
    },
    deletetodo(id) {
      this.customFilter('all');
      this.db.get(`${id}`)
      .then((doc) => this.db.remove(doc))
      .then(() => { 
          console.log('todo removed');
          this.todos = this.backupTodos.filter((i) => i._id != id);
          if (this.todos.length > 0) {
            this.backupTodos = this.todos;
          } else {
        this.backupTodos = [];
      }
        })
      .catch(error => console.log(error));
    },
  },
  data() {
    return {
      todos: [],
      backupTodos: [],
      db: null,
      active: "all",
    };
  },
  mounted() {
    this.db = new PouchDB("Todos");
    this.db
      .allDocs({ include_docs: true })
      .then((r) => {
        r.rows.forEach((d) => {
          this.todos.push(d.doc);
        });
        this.backupTodos = this.todos;
      })
      .catch((error) => console.log(error));
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
