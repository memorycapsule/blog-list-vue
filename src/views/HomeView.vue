<template>
  <div class="contain">
    <div class="home">
      <TodoCreator @create-todo="createTodo" />
      <ul class="todo-list" v-if="todoList.length > 0">
        <TodoItem
          v-for="(todo, index) in todoList"
          :todos="todo"
          :key="index"
          :id="index"
          @delete-todo="deleteTodo"
          @edit-todo="editTodo"
          @complete-todo="completeTodo"
        />
      </ul>
      <p v-else class="todos-msg">
        <span>Add some todo's to complete!</span>
      </p>
    </div>
  </div>
</template>
<style lang="scss" scoped>
.contain {
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: flex-start;
}
.home {
  border: 1px solid;
  box-shadow: 1px 1px black;
  min-width: 400px;
  max-height: 300px;
  overflow-y: scroll;
  .todo-list {
    align-items: center;
  }
  ul {
    display: flex;
    padding: 5px 0 0 0;
    margin: 0;
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
    todo: todo,
    isCompleted: false,
  });
  console.log(todoList.value);
};

const deleteTodo = (id) => {
  console.log("deletefunc");
  todoList.value.splice(id, 1);
  console.log(todoList.value);
};

const editTodo = (todo) => {
  console.log(todo.id);
};

const completeTodo = (id) => {
  todoList.value[id].isCompleted = !todoList.value[id].isCompleted;
};
</script>
