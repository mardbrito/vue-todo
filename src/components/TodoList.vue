<script setup>
defineProps({
  todos: {
    type: Object,
    required: true,
  },
});

defineEmits(["delete-todo"]);
</script>

<template>
  <li v-for="todo in todos" :key="todo.id">
    <input type="checkbox" v-model="todo.completed" />
    <span :class="{ done: todo.completed }">{{ todo.task }}</span>
    <button @click="$emit('delete-todo', todo.id)">x</button>
  </li>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
