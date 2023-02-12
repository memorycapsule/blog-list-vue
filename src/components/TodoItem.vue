<script setup>
import { ref, defineProps } from "vue";

defineProps({ todos: Object });
const newTodo = ref("");
const isEditing = null;

const toggleEdit = (todo) => {
  todo.value.isEditing = !todo.value.isEditing;
};
</script>

<template>
  <li>
    <div class="todo">
      <span> {{ todos.todo }}</span>

      <div class="actions">
        <button @click="$emit('delete-todo', todos.todo)">delete</button>

        <button @click="toggleEdit(todos.todo)">Edit</button>
        <input
          v-if="isEditing"
          type="text"
          @input="$emit('edit-todo', [newTodo, todosvalue.indexOf(todos.todo)])"
        />
      </div>
    </div>
  </li>
</template>

<style lang="scss" scoped>
li {
  height: 50px;
  width: 300px;
  list-style-type: none;
  margin: 0;
  padding: 0;
  .todo {
    display: flex;
    justify-content: center;

    span {
      background-color: lightgrey;
      border-radius: 15px;
      padding: 5px;
      margin: auto auto auto 0px;
      justify-content: space-between;
      font-weight: bold;
      color: #2c3e50;
      overflow-y: scroll;
      overflow-x: auto;
      column-span: all;
    }

    .actions {
      display: flex;
      justify-content: center;
      align-items: center;
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
  }
}
</style>
