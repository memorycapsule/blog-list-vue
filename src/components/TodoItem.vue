<script setup>
import { ref, defineProps } from "vue";
const newTodo = ref("");
defineProps({ todos: Object, id: Number });
const toggleEdit = (todo) => {
  todo.isEditing = !todo.isEditing;
};
</script>

<template>
  <li>
    <div class="todo">
      <span
        v-if="!todos.isEditing"
        @click="$emit('complete-todo', id)"
        :class="{
          'completed-todo': todos.isCompleted,
        }"
        >{{ todos.todo }}</span
      >
      <input
        v-if="todos.isEditing"
        v-model="newTodo"
        @change="$emit('edit-todo', id, newTodo), toggleEdit(todos)"
      />
      <div class="actions">
        <button @click="$emit('delete-todo', id)">delete</button>
        <button @click="toggleEdit(todos)">Edit</button>
      </div>
    </div>
  </li>
</template>

<style lang="scss" scoped>
li {
  height: 50px;
  width: 300px;
  list-style-type: none;
  margin: 0 15px 0 15px;
  padding: 0;

  .todo {
    display: flex;
    justify-content: center;

    .completed-todo {
      text-decoration: line-through;
    }

    span {
      padding: 5px;
      margin: auto auto auto 0px;
      justify-content: space-between;
      font-weight: bold;
      color: #2c3e50;
      overflow-y: scroll;
      overflow-x: auto;
      column-span: all;
    }

    input {
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
        height: 100%;
        margin: 0px 0px 0px auto;
        border: none;
        color: grey;
        text-align: center;
        text-decoration: none;
        display: inline-block;
        text-transform: uppercase;
        &:hover {
          cursor: pointer;
        }
      }
    }
  }
}
</style>
