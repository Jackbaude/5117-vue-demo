<template>
  <div>
    <h1>Todo List</h1>
    <TodoCreation @add-todo="addTodo" />
    <div>
      <label for="filter">Filter: </label>
      <select id="filter" v-model="filter">
        <option value="all">All</option>
        <option value="complete">Complete</option>
        <option value="incomplete">Incomplete</option>
      </select>
    </div>
    <TodoItem
      v-for="item in filteredTodos"
      :key="item.id"
      :todo="item"
      @update-status="updateTodoStatus"
      @delete-todo="deleteTodo"
    />
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
import TodoItem from "./TodoItem.vue";
import TodoCreation from "./TodoCreation.vue";

const todos = ref([
  {
    id: 0,
    title: "Write a blog post",
    description: "Draft a blog post about the recent project milestones.",
    status: "incomplete",
    due_date: "2024-12-02",
    priority: "high",
  },
  {
    id: -1,
    title: "Complete Vue project",
    description: "Finish the Vue-based todo app.",
    status: "complete",
    due_date: "2024-12-05",
    priority: "medium",
  },
]);

const filter = ref("all");

const filteredTodos = computed(() => {
  if (filter.value === "all") return todos.value;
  return todos.value.filter((todo) => todo.status === filter.value);
});

const addTodo = (newTodo) => {
  todos.value.push(newTodo);
};

const updateTodoStatus = (id) => {
  const todo = todos.value.find((item) => item.id === id);
  if (todo) {
    todo.status = todo.status === "complete" ? "incomplete" : "complete";
  }
};

const deleteTodo = (id) => {
  todos.value = todos.value.filter((item) => item.id !== id);
};
</script>
