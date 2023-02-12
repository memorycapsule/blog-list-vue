<template>
  <div class="home">
    <TodoCreator @create-todo="createTodo" />
    <ul class="todo-list" v-if="todoList.length > 0">
      <TodoItem
        v-for="todo in todoList"
        :todos="todo"
        :key="todo.id"
        @delete-todo="deleteTodo"
        @edit-todo="editTodo"
      />
    </ul>
    <p v-else class="todos-msg">
      <span>Add some todo's to complete!</span>
    </p>
  </div>
</template>
<style lang="scss" scoped>
.home {
  .todo-list {
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
  }
  ul {
    display: flex;
    justify-content: center;
    overflow-y: scroll;
    flex-direction: column;
    flex-grow: 1;
  }
}
</style>
<script setup>
import TodoCreator from "@/components/TodoCreator.vue";
import TodoItem from "@/components/TodoItem.vue";

import { ref } from "vue";

const todoList = ref([]);
const createTodo = (todo) => {
  todoList.value.push({
    id: todoList.value.length,
    todo: todo,
    isCompleted: false,
    isEditing: false,
  });
  console.log(todoList.value);
};

const deleteTodo = (todo) => {
  console.log("deletefunc");
  todoList.value.splice(todoList.value.indexOf(todo), 1);
  console.log(todoList.value);
};

const editTodo = (todo) => {
  console.log(todo);
};
</script>
