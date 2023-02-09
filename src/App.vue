<script>
import { ref } from "vue";

export default {
  name: "App",
  setup() {
    const newTodo = ref("");
    const dateDue = ref("dateDue");
    const date = new Date();
    const author = ref("");
    const dateTimeDisplay =
      date.getFullYear() + "-" + (date.getMonth() + 1) + "-" + date.getDate();
    const todosData = JSON.parse(localStorage.getItem("todos"));
    const todos = ref(todosData);

    function addTodo() {
      console.log(dateDue);
      if (newTodo.value) {
        todos.value.push({
          done: false,
          content: newTodo.value,
          author: author,
          date_created: dateTimeDisplay,
          date_due: dateDue.value,
        });
        newTodo.value = "";
        dateDue.value = dateTimeDisplay;
      }
      saveTodo();
    }
    function removeTodo(index) {
      todos.value.splice(index, 1);
      saveTodo();
    }
    function doneTodo(todo) {
      todo.done = !todo.done;
      saveTodo();
    }
    function editTodo() {
      // todo, funny
    }
    function saveTodo() {
      const store = JSON.stringify(todos.value);
      localStorage.setItem("todos", store);
    }
    return {
      todos,
      newTodo,
      dateDue,
      author,
      addTodo,
      removeTodo,
      doneTodo,
      editTodo,
      saveTodo,
    };
  },
};
</script>

<template>
  <div class="header">
    <h1>Todo App</h1>
  </div>

  <div class="inputs">
    <form @submit="addTodo()">
      <label>
        Insert a new Todo
        <div class="input_todo">
          <input
            v-model="newTodo"
            name="newTodo"
            style="width: 200px; height: 30px; resize: none; outline: none"
          />
          <input v-model="dateDue" name="dateDue" type="date" />
          <button>add todo</button>
        </div>
      </label>
    </form>
  </div>
  <h2>Your current todos</h2>

  <div class="list">
    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        <div class="dates">
          <p class="date_created">Created: {{ todo.date_created }}</p>
          <p class="date_created">Due: {{ todo.date_due }}</p>
        </div>
        <div class="todo">
          <div>
            <p :class="{ done: todo.done }" @click="doneTodo(todo)">
              {{ todo.content }}
            </p>
          </div>
          <input type="checkbox" @click="removeTodo(index)" />
        </div>
      </li>
    </ul>
  </div>

  <RouterView />
</template>

<style scoped>
.header {
  display: flex;
  justify-content: center;
}
.inputs {
  display: flex;
}
i .list {
  display: inline-flex;
}

.list ul {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  grid-gap: 10px 10px;
}
.todo {
  display: flex;
  flex-direction: row;
}
.todo p {
  cursor: pointer;
}
.input_todo {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}
input {
  justify-content: flex-end;
  /* margin-left: auto; */
}

.dates {
  display: flex;
  justify-content: space-between;

  font-size: 9px;
  background-color: rgb(41, 40, 40);
  border-radius: 20px;
}

.done {
  text-decoration: line-through;
  color: grey;
}

.list li {
  color: white;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  width: 100%;
  border: 2px solid white;
  padding: 12px;
  /* margin-bottom: 15px; */
}
</style>
