<script setup>
import { computed, onMounted, ref, watch } from "vue";
import TodoForm from "./TodoForm.vue";
import TodoList from "./TodoList.vue";
import TodoFilter from "./TodoFilter.vue";
import TodosLeft from "./TodosLeft.vue";

let todos = ref([]);
const activeFilter = ref("all");

onMounted(() => {
  todos.value = JSON.parse(localStorage.getItem("vue-todos")) || [];
});

function generateId() {
  return Math.random().toString(16).slice(2);
}

function addTodo(task) {
  let newTodo = {
    id: generateId(),
    task,
    completed: false,
  };
  todos.value.push(newTodo);
}

function deleteTodo(id) {
  todos.value = todos.value.filter((todo) => todo.id !== id);
}

function filterTodo(type) {
  return (activeFilter.value = type);
}

watch(
  todos,
  (newVal) => {
    localStorage.setItem("vue-todos", JSON.stringify(newVal));
  },
  { deep: true }
);

// computeds
const filteredTodos = computed(() => {
  const items =
    activeFilter.value === "all"
      ? (item) => item
      : activeFilter.value === "completed"
      ? (item) => item.completed
      : (item) => !item.completed;

  return todos.value.filter(items);
});

const todosLeft = computed(() => {
  return todos.value.filter((todo) => !todo.completed).length;
});

const todosAmount = computed(() => {
  return todos.value.length;
});
</script>

<template>
  <h1>todos</h1>

  <TodoForm @add-todo="(name) => addTodo(name)" :todos-amount="todosAmount" />
  <TodoFilter
    :active-filter="activeFilter"
    @filter-todo="(filter) => filterTodo(filter)"
  />
  <TodosLeft :todosLeft="todosLeft" />

  <ul class="tasks">
    <TodoList :todos="filteredTodos" @delete-todo="(id) => deleteTodo(id)" />
  </ul>
</template>
