<script setup>
defineProps({
  todosLeft: {
    type: Number,
  },
});
</script>

<template>
  <span v-if="todosLeft === 0"> No todos to be done! </span>
  <span v-else>
    {{ todosLeft }}
    {{ todosLeft === 1 ? "todo" : "todos" }} left
  </span>
</template>
