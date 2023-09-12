<script setup lang="ts">
import { ref } from 'vue';

let id = 0;

const newTodo = ref('');
// TODO: How to enforce a type for a task?
const todos = ref([{ id: id++, text: 'Default text' }]);

function addTodo() {
  // TODO: Parse value here
  todos.value.push({ id: id++, text: newTodo.value });
  newTodo.value = '';
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => todo !== t);
}
</script>

<template>
  <div class="body">
    <form @submit.prevent="addTodo">
      <input v-model="newTodo" />
      <button>Add Todo</button>
    </form>
    <ul>
      <li v-for="todo in todos" :key="todo.id">
        {{ todo.text }}
        <button @click="removeTodo(todo)">X</button>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.body {
  display: flex;
  flex-direction: column;
}
.done {
  text-decoration: line-through;
}
</style>
