<script setup>
import { ref } from "vue";

defineEmits(["filter-todo"]);
defineProps({
  activeFilter: {
    type: String,
    required: true,
  },
});

const filters = ref(["all", "completed", "active"]);
</script>

<template>
  <div class="tags">
    <span v-for="(filter, index) in filters" :key="index">
      <span
        @click="$emit('filter-todo', filter)"
        :class="{ active: filter === activeFilter }"
        >{{ filter }}</span
      >
    </span>
  </div>
</template>

<style scoped>
.tags {
  margin-top: 10px;
  padding: 5px 0;
}

.tags span {
  padding: 3px 6px;
}
.active {
  text-decoration: underline;
}
</style>
