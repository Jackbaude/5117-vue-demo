<template>
  <div class="todo-list">
    <h1>Todo List</h1>
    
    <!-- Input for new todo -->
    <input 
      v-model="newTodo" 
      @keyup.enter="addTodo" 
      placeholder="Enter a new todo"
    />
    <button @click="addTodo">Add Todo</button>

    <!-- Conditional rendering with v-if -->
    <p v-if="todos.length === 0">No todos yet! Add some tasks.</p>

    <!-- v-for to render todo list -->
    <ul v-else>
      <li 
        v-for="(todo, index) in todos" 
        :key="index" 
        class="todo-item"
      >
        {{ todo }}
        <button @click="removeTodo(index)">Delete</button>
      </li>
    </ul>

    <!-- Another v-if example -->
    <p v-if="todos.length > 5">
      Wow, you have more than 5 todos! You're productive!
    </p>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// Create a reactive reference for todos
const todos = ref([])

// Create a reactive reference for new todo input
const newTodo = ref('')

// Method to add a new todo
const addTodo = () => {
  if (newTodo.value.trim()) {
    todos.value.push(newTodo.value.trim())
    newTodo.value = '' // Clear input after adding
  }
}

// Method to remove a todo
const removeTodo = (index) => {
  todos.value.splice(index, 1)
}
</script>

<style scoped>
.todo-list {
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
}

input {
  width: 100%;
  padding: 8px;
  margin-bottom: 10px;
}

ul {
  list-style-type: none;
  padding: 0;
}

.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  border-bottom: 1px solid #eee;
}

button {
  margin-left: 10px;
  padding: 5px 10px;
}
</style>