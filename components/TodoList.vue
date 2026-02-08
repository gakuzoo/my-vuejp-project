<script setup>
const props = defineProps({
  todos: Array,
});
const emit = defineEmits(['checkTodoEvent','deleteTodoEvent']);
function handleCheck(todo) {
  emit('checkTodoEvent', todo);
}
function handleClick(todo) {
  emit('deleteTodoEvent', todo);
}
</script>

<template>
  <ul>
    <li v-for="todo in todos" :key="todo.id">
      <label>
        <input type="checkbox" :checked="todo.isCompleted"
         @click="handleCheck(todo)">
        {{ todo.title }}
      </label>
      <button @click="handleClick(todo)">Delete</button>
    </li>
  </ul>
</template>

<style scoped>
ul {
  margin: 0;
  padding: 0;
  list-style: none;
}

label:has(:checked){
  color: #ccc;
  text-decoration: line-through;
}

li + li {
  margin-top: 4px;
}

li {
  display: flex;
  gap: 8px;
}

button {
  margin-left: auto;
}
</style>
