<script setup>
import { ref } from 'vue';
const emit = defineEmits(['addTodoEvent'])
const newTodo = ref();

function handleSubmit() {
  if (newTodo.value.trim() === '') {
    return;
  }
  emit('addTodoEvent', newTodo.value);
  newTodo.value = '';
}

</script>

<template>
  <form @submit.prevent="handleSubmit">
      <input type="text" v-model="newTodo">
      <button>Add</button>
    </form>
</template>

<style scoped>
form {
  margin-top: 16px;
  display: flex;
  gap: 4px;
}

input {
  flex: 1;
  padding: 4px;
}
</style>
