<template>
  <div>
    <div class="status">
      <span class="ml-5">Items left:</span>
      <span>{{this.todoLeft}}</span>
      |
      <span class="cursor" @click="$emit('all')">All todos</span> |
      <span class="cursor" @click="$emit('left')">Left todos</span> |
      <span class="cursor" @click="$emit('done')">Done todos</span>
    </div>
  </div>
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
.ml-5 {
  margin-left: 5px;
}
.active {
  text-shadow: blueviolet 0px 0px 2px;
}
.status span:nth-child(2) {
  color: red;
}
.cursor {
  cursor: pointer;
}
.cursor:hover {
  text-shadow: green 1px 1px 2px;
}
.status {
  width: 350px;
  margin: auto;
  border-bottom: 2px solid green;
  border-top: 2px solid green;
  margin-top: 20px;
  height: 1.2rem;
  text-align: left;
  background-color: khaki;
  border-radius: 5px;
}
</style>