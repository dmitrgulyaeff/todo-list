<script setup lang="ts">
import { ref } from 'vue';
import { defaultTodos } from './constants';
import type { TTodo } from './types';
import todoListItem from './-item/todo-list-item.vue';
import todoListInput from './-input/todo-list-input.vue';

const showOnlyChecked = ref(false);

const filterTodo = (t: TTodo) => {
  return !showOnlyChecked.value || t.completed;
};

const todos = ref<TTodo[]>(defaultTodos);
let id = todos.value.length;
const addTodo = (title: TTodo['title']) => {
  const newTodo: TTodo = {
    completed: false,
    id: ++id,
    title,
    userId: 1,
  };

  todos.value.push(newTodo);
};

const deleteTodo = (todo: TTodo) => {
  todos.value = todos.value.filter((td) => td.id !== todo.id);
};
</script>

<template>
  <ul>
    <todoListItem
      v-for="(todo, index) in todos"
      :key="todo.id"
      v-model:todo="todos[index]"
      :is-checked="filterTodo"
      @delete:todo="deleteTodo"
    />
  </ul>
  <todoListInput @add-todo="addTodo" />
  <div>
    Show only checked
    <input
      v-model="showOnlyChecked"
      type="checkbox"
    >
  </div>
</template>

<script></script>
