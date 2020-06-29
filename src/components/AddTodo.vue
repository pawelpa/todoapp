<template>
  <div>
    <form class="form" @submit.prevent="localEmit()">
      <input type="text" v-model="value" maxlength="36" placeholder="Enter todo here..." />
      <button type="submit">Add</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "AddTodo",
  data() {
    return {
      value: ""
    };
  },
  methods: {
    localEmit() {
      if (this.value === "") {
        alert("Please enter valid todo item");
        return;
      }
      this.$emit("addtodo", this.value);
      this.value = "";
    }
  }
};
</script>

<style scoped>
.form {
  display: flex;
  flex-direction: row;
  justify-content: center;
  margin-bottom: 20px;
}
.form input {
  padding: 2px;
  border: none;
  border-bottom: 2px solid green;
  width: 240px;
  outline: none;
  font-size: 1rem;
}
button {
  background-color: khaki;
  color: green;
  border: solid 2px green;
  width: 80px;
  height: 30px;
  font-size: 0.9rem;
  /* border-bottom: 2px solid green; */
}
</style>