<template>
  <div class="input-list">
    <input @input="handleChange" type="text" v-model="todo" />
    <button @click="valid ? $emit('create-todo', todo) : notValid">
      create
    </button>
  </div>
</template>
<script setup>
import { ref } from "vue";
const todo = ref("");
var valid = false;
const handleChange = () => {
  console.log("test");
  if (todo.value !== "") {
    valid = true;
  } else {
    valid = false;
  }
};
</script>

<style lang="scss" scoped>
.input-list {
  input {
    border: none;
    background-color: #3cbc8d;
    color: white;
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
