<script setup>
import { ref, defineProps } from "vue";

defineProps({ todos: Object, id: Number });
const newTodo = ref("");

// const toggleEdit = (todo) => {
//   todo.value.isEditing = !todo.value.isEditing;
// };
</script>

<template>
  <li>
    <div class="todo">
      <span
        @click="$emit('complete-todo', id)"
        :class="{
          'completed-todo': todos.isCompleted,
        }"
        >{{ todos.todo }}</span
      >

      <div class="actions">
        <button @click="$emit('delete-todo', id)">delete</button>

        <button @click="toggleEdit(todos.todo)">Edit</button>
        <input
          v-if="false"
          type="text"
          @input="$emit('edit-todo', { newValue: newTodo, id: id })"
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
