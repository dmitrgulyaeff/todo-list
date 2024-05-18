<script setup lang="ts">
import type { TTodo } from '../types';

const todo = defineModel<TTodo>('todo');

defineEmits<{
  'delete:todo': [TTodo];
}>();
</script>

<template>
  <li v-if="todo">
    <label
      :for="'todo-' + todo.id"
      :class="{ label: true, label_checked: todo.completed }"
    >
      {{ todo.title }}
      <input
        :id="'todo-' + todo.id"
        v-model="todo.completed"
        type="checkbox"
      >
    </label>
    <button @click="$emit('delete:todo', todo)">
      delete
    </button>
  </li>
</template>

<style scoped>
.label_checked {
  text-decoration: line-through;
}
</style>
