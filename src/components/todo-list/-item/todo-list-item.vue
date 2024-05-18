<script setup lang="ts">
import { computed } from 'vue';
import type { TTodo } from '../types';

const props = defineProps<{
  todo: TTodo,
}>();

const emit = defineEmits<{
  'update:todo': [TTodo];
  'delete:todo': [TTodo];
}>();

const proxyTodo = computed({
  get() {
    return props.todo;
  },
  set(newTodo) {
    emit('update:todo', newTodo);
  },
});
</script>

<template>
  <li>
    <label
      :for="'todo-' + todo.id"
      :class="{'label' : true, 'label_checked' : proxyTodo.completed}"
    >
      {{ todo.title }}
      <input
        :id="'todo-' + todo.id"
        v-model="proxyTodo.completed"
        type="checkbox"
      >
    </label>
    <button @click="emit('delete:todo', todo)">
      delete
    </button>
  </li>
</template>

<style scoped>
.label {

}

.label_checked {
  text-decoration: line-through
}
</style>
