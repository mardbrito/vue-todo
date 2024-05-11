<script setup>
import { ref } from "vue";

let todo = ref("");
const emit = defineEmits(["add-todo"]);
defineProps({
  todosAmount: {
    type: Number,
    required: true,
  },
});

function handleSubmit() {
  if (!todo.value.trim()) return;

  emit("add-todo", todo.value);
  todo.value = "";
}
</script>

<template>
  <form @submit.prevent="handleSubmit">
    <input
      type="text"
      placeholder="What do you have to be done?"
      v-model="todo"
    />
  </form>
</template>
