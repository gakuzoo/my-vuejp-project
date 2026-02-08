<script setup>
import { onMounted, reactive, watch } from 'vue';
import TodoListVue from './components/TodoList.vue';
import TodoAddFormVue from './components/TodoAddForm.vue';

const todos = reactive([]);

function addTodo(title) {
  todos.push({
    id: crypto.randomUUID,
    title: title,
    isCompleted: false,
  })
}
function toggleCheckbox(todo) {
  const index = todos.findIndex((element) => {
    return element.id === todo.id;
  });

  todos[index].isCompleted = !todos[index].isCompleted;
}
function deleteTodo(todo) {
  if (confirm('削除してよいですか？') === false) {
    return;
  }
  const index = todos.findIndex((element) => {
    return element.id === todo.id;
  });

  todos.splice(index, 1);
}

onMounted(() => {
  const savedTodos = localStorage.getItem('todos');

  if (savedTodos !== null) {
    const parsedTodos = JSON.parse(savedTodos);

    parsedTodos.forEach((todo) => {
      todos.push(todo);
    });
  }
});

watch(todos, (updatedTodos) => {
  localStorage.setItem('todos', JSON.stringify(updatedTodos));
});
</script>

<template>
  <div class="container">
    <h1>Todos</h1>
    <TodoListVue :todos="todos" 
      @checkTodoEvent="toggleCheckbox"
      @deleteTodoEvent="deleteTodo"
     />
    <TodoAddFormVue @addTodoEvent="addTodo" />
  </div>
</template>

<style scoped>
.container{
  width:400px;
  margin:0 auto;
}

h1{
  font-size: 20px;
  border-bottom: 3px solid green;
  padding-bottom: 8px;
}
</style>
