<script setup lang="ts">
import { ref } from 'vue';

  const emit = defineEmits<{
    addTodo: [string];
  }>();

  const title = ref('')
  
  const handleSubmit = (e : SubmitEvent) =>{
    e.preventDefault();
    emit('addTodo', title.value)
    title.value = ''
  }
</script>

<template>
  <form @:submit="handleSubmit">
    <input
      v-model="title"
      type="string"
    >
    <button>Add Todo</button>
  </form>
</template>
