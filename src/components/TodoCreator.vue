<template>
  <div class="input-list">
    <input type="text" v-model="todo" />
    <button @click="callEmit">create</button>
  </div>
</template>
<script setup>
import { ref, defineEmits } from "vue";
const todo = ref("");
// var valid = false;

const emit = defineEmits(["create-todo"]);
const callEmit = () => {
  console.log("fire");
  emit("create-todo", todo.value);
};
// const handleChange = () => {
//   if (todo.value !== "") {
//     valid = true;
//   } else {
//     valid = false;
//   }
// };
</script>

<style lang="scss" scoped>
.input-list {
  input {
    margin: 5px;
    border: none;
    background-color: #e9e9ed;
    color: black;
  }
  &.input-err {
    border-color: red;
  }

  button {
    margin: 0px 0px 0px auto;
    border: none;
    color: grey;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    text-transform: uppercase;
  }
}
</style>
