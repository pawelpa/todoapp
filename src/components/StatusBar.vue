<template>
  <div class="status">Todo left: {{this.todoLeft}}</div>
</template>

<script>
export default {
  props: {
    todos: Array,
  },
  computed: {
    todoLeft() {
      return this.todos.filter((t) => t.done !== true).length;
    },
  },
};
</script>

<style scoped>
.status {
  width: 350px;
  margin: auto;
  border-bottom: 2px solid green;
  border-top: 2px solid green;
  margin-top: 20px;
  height: 1.2rem;
  text-align: left;
  background-color: khaki;
}
</style>