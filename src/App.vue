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
    <StatusBar 
    v-on:all="customFilter('all')"
    v-on:left="customFilter('left')"
    v-on:done="customFilter('done')"
    :todos="todos" />
  </div>
</template>

<script>
import Todo from "./components/Todo.vue";
import AddTodo from "./components/AddTodo.vue";
import StatusBar from "./components/StatusBar.vue";
import {v4 as uuid} from 'uuid';
export default {
  name: "App",
  components: {
    Todo,
    AddTodo,
    StatusBar,
  },
  methods: {
    customFilter(what) {
       switch(what) {
         case 'done': console.log('done');
                this.todos = this.backupTodos.filter((t)=>t.done === true)
          break;
         case 'all': console.log('all');
            if(this.backupTodos.length > this.todos.length) {
                  this.todos = this.backupTodos;
              }
         break;
         case 'left': console.log('left');
               this.todos = this.backupTodos.filter((t)=>t.done !== true )
         break;
       }
    },
    addtodo(todo) {
      this.todos = [
        ...this.todos,
        { id: uuid(), text: todo, done: false },
      ];
      //console.log(todo);
      this.backupTodos = this.todos;
    },
    checktodo(id) {
      console.log(id);
      this.todos.forEach((todo) => {
        if (todo.id === id) {
          return (todo.done = !todo.done);
        }
      });
      this.backupTodos = this.todos;
    },
    deletetodo(id) {
      this.todos = this.todos.filter((i) => i.id != id);
      this.backupTodos = this.tods;
    },
  },
  data() {
    return {
      todos: [
        { id: uuid(), text: "Todo one", done: false },
        { id: uuid(), text: "Todo two", done: true },
      ],
      backupTodos: [],
    };
  },
  mounted() {
    this.backupTodos = this.todos;
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
h1 {
  margin-bottom: 50px;
}
</style>
