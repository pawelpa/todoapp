<template>
  <div>
    <div class="status">
      <span class="ml-5">Items left:</span>
      <span>{{this.todoLeft}}</span>
      |
      <span title="Show all todos" class="cursor" :class="{ active: active=='all'}" @click="$emit('all')">All todos</span> |
      <span title="Show remaining todos" class="cursor" :class="{ active: active=='left'}" @click="$emit('left')">Left todos</span> |
      <span title="Show completed todos" class="cursor" :class="{ active: active=='done'}" @click="$emit('done')">Done todos</span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    todos: Array,
    active: String,
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
  text-shadow: green 0px 0px 2px;
}
.status span:nth-child(2) {
  color: green;
  font-weight: 600;
  margin-left: 2px;
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