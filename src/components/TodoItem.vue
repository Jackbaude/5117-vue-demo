<template>
  <div class="todo-item">
    <h3 :class="{ completed: todo.status === 'complete' }">{{ todo.title }}</h3>
    <p v-if="todo.priority">Priority: {{ todo.priority }}</p>
    <p>{{ todo.description }}</p>
    <small>Due: {{ todo.due_date }}</small>
    <div>
      <button @click="toggleStatus">
        {{ todo.status === 'complete' ? 'Mark Incomplete' : 'Mark Complete' }}
      </button>
      <button @click="deleteTodo" class="delete-btn">Delete</button>
    </div>
  </div>
</template>

<script setup>

const props = defineProps({
  todo: {
    type: Object,
    required: true,
  },
});

const emit = defineEmits(["update-status", "delete-todo"]);

const toggleStatus = () => {
  emit("update-status", props.todo.id);
};

const deleteTodo = () => {
  emit("delete-todo", props.todo.id);
};
</script>

<style scoped>
.todo-item {
  border: 1px solid #ccc;
  padding: 10px;
  margin: 10px 0;
  border-radius: 5px;
}

.completed {
  text-decoration: line-through;
  color: gray;
}

.delete-btn {
  color: white;
  background-color: red;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
  border-radius: 3px;
  margin-left: 10px;
}

.delete-btn:hover {
  background-color: darkred;
}
</style>
