<script setup>
import { ref } from 'vue'

const newTodo = ref('') //Creates a variable for the input box.
const todos = ref([]) //Creates a variable for the list of todos.

const backToHome = () => {
  window.location.href = 'hello'
}

const addTodo = () => {
  if (newTodo.value.trim() === '') return

  todos.value.push({
    id: Date.now(),
    text: newTodo.value,
    done: false
  })

  newTodo.value = ''
}

const removeTodo = (id) => {
  todos.value = todos.value.filter(todo => todo.id !== id)
}
</script>

<template>
  <div class="todo-container">
    <h1> 📝To-Do List</h1>
    <button @click="backToHome">back to home</button>

    <input
      v-model="newTodo"
      @keyup.enter="addTodo"
      placeholder="add your task"
    />

    <button @click="addTodo">Add</button>

    <ul>
      <li v-for="todo in todos" :key="todo.id">
        <input type="checkbox" v-model="todo.done" />
        <span :class="{ done: todo.done }">
          {{ todo.text }}
        </span>
        <button @click="removeTodo(todo.id)">❌</button>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.todo-container {
  max-width: 400px;
  margin: 40px auto;
  font-family: Arial, sans-serif;
}

input {
  padding: 8px;
  width: 70%;
}

button {
  margin-left: 5px;
  padding: 8px;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  display: flex;
  align-items: center;
  margin-top: 10px;
}

.done {
  text-decoration: line-through;
  color: gray;
}
</style>
