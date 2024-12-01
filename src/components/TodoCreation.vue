<template>
  <div class="todo-creation">
    <h2>Create a New Todo</h2>
    <form @submit.prevent="createTodo">
      <div>
        <label for="title">Title:</label>
        <input id="title" v-model="newTodo.title" required />
      </div>
      <div>
        <label for="priority">Priority:</label>
        <select id="priority" v-model="newTodo.priority">
          <option value=""></option>
          <option value="low">Low</option>
          <option value="medium">Medium</option>
          <option value="high">High</option>
        </select>
      </div>
      <div>
        <label for="description">Description:</label>
        <textarea id="description" v-model="newTodo.description" required></textarea>
      </div>
      <div>
        <label for="due_date">Due Date:</label>
        <input id="due_date" type="date" v-model="newTodo.due_date" required />
      </div>
      <button type="submit">Add Todo</button>
    </form>
  </div>
</template>

<script setup>
import { ref } from "vue";

const emit = defineEmits(["add-todo"]);
const id = ref(1);

const newTodo = ref({
  title: "",
  description: "",
  due_date: "",
});

const createTodo = () => {
  
  if (newTodo.value.title && newTodo.value.description && newTodo.value.due_date) {
    emit("add-todo", {
      id: id.value++,
      title: newTodo.value.title,
      priority: newTodo.value.priority,
      description: newTodo.value.description,
      due_date: newTodo.value.due_date,
      status: "incomplete",
    });
    newTodo.value = { priority: "",title: "", description: "", due_date: "" }; // Reset the form
  }
};
</script>

<style scoped>
.todo-creation {
  margin: 20px 0;
  padding: 20px;
  border: 1px solid #444;
  border-radius: 8px;
  background-color: #1e1e1e;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.5);
  color: #f5f5f5;
  min-width: 400px;
}

.todo-creation h2 {
  margin-bottom: 15px;
  font-size: 1.5rem;
  color: #f5f5f5;
}

form div {
  margin-bottom: 15px;
}

form label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
  color: #ddd;
}

form input,
form textarea {
  width: 100%;
  padding: 8px;
  border: 1px solid #555;
  border-radius: 4px;
  box-sizing: border-box;
  font-size: 1rem;
  background-color: #2a2a2a;
  color: #f5f5f5;
}

form input:focus,
form textarea:focus {
  border-color: #007bff;
  outline: none;
  box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
}

button {
  background-color: #007bff;
  color: white;
  padding: 8px 15px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1rem;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #0056b3;
}

button:active {
  background-color: #004085;
  box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.5);
}
</style>


