<template>
  <div>
    <div class="todo" :class="{ done: done }">
      <input type="checkbox" v-model="done" :id="todo._id" />
      <label
        title="Click to mark as complete"
        :for="todo._id"
        v-on:click="$emit('checktodo', todo._id)"
        >{{ todo.text }}</label
      >
      <span>
        <button
          title="Remove"
          class="btn"
          v-on:click="$emit('deletetodo', todo._id)"
        >
          &times;
        </button>
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: "Todo",
  props: {
    todo: Object,
  },
  data() {
    return {
      done: this.todo.done,
    };
  },
};
</script>

<style scoped>
.todo {
  display: grid;
  grid-template-columns: 0.5fr 6fr 1fr;
  grid-template-rows: minmax(50px);
  width: 350px;
  border-bottom: 2px solid green;
  margin: auto;
  margin-top: 5px;
  background-color: khaki;
  text-align: center;
  overflow: hidden;
  cursor: pointer;
  position: relative;
  border-radius: 5px;
}

.btn {
  background-color: khaki;
  border: none;
  font-size: 1.2rem;
  cursor: pointer;
  outline: none;
}

.btn:hover {
  border: 1px dashed green;
  border-radius: 50%;
  transform: scale(0.60);

}
.btn:active {
  border: 2px solid green;
  border-radius: 50%;
  transform: scale(0.70);
}
.done {
  text-decoration: line-through;
}
/* Hide the browser's default checkbox */
.todo input[type="checkbox"] {
  opacity: 0;
}

.todo label {
  position: relative;
  display: inline-block;
  word-wrap: normal;
  cursor: pointer;
  /*16px width of fake checkbox + 6px distance between fake checkbox and text*/
  padding-left: 22px;
}

.todo label::before,
.todo label::after {
  position: absolute;
  content: "";

  /*Needed for the line-height to take effect*/
  display: inline-block;
}

/*Outer box of the fake checkbox*/
.todo label::before {
  height: 16px;
  width: 16px;
  border-radius: 5px;
  border: 1px dashed;
  left: 0px;

  /*(24px line-height - 16px height of fake checkbox) / 2 - 1px for the border
     *to vertically center it.
     */
  top: 3px;
}

/*Checkmark of the fake checkbox*/
.todo label::after {
  height: 5px;
  width: 9px;
  border-left: 2px solid;
  border-bottom: 2px solid;

  transform: rotate(-45deg);
  color: green;
  left: 4px;
  top: 7px;
}

/*Hide the checkmark by default*/
.todo input[type="checkbox"] + label::after {
  content: none;
}

/*Unhide on the checked state*/
.todo input[type="checkbox"]:checked + label::after {
  content: "";
}

/*Adding focus styles on the outer-box of the fake checkbox*/
/* .todo input[type="checkbox"]:focus + label::before {
  outline: rgb(59, 153, 252) auto 5px;
} */
label {
  font-size: 0.9rem;
  overflow: hidden;
  padding: 2px;
}
</style>
