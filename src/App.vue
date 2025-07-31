<!-- Composition APIの書き方 -->

<script setup>
import { ref } from 'vue'
import TodoInput from './TodoInput.vue'
import TodoItem from './TodoItem.vue'

const todos = ref([
  { isDone: false, text: '牛乳' },
  { isDone: false, text: '卵' },
  { isDone: false, text: 'パン' },
  { isDone: false, text: '肉' },
])

function addTodo(newTodoText) {
  if (newTodoText === '') return alert('文字を入力してください')
  todos.value.push({ isDone: false, text: newTodoText })
}

function clearDoneTodos() {
  todos.value = todos.value.filter((todo) => !todo.isDone)
}
</script>

<template>
  <div class="todo-wrapper">
    <h1>My ToDo App</h1>
    <TodoInput @add-todo="addTodo" @clear-todo="clearDoneTodos" />
    <p v-if="todos.length === 0">Todoはまだありません</p>
    <ul>
      <TodoItem
        v-for="(todo, index) in todos"
        :key="index"
        :todo="todo"
        @update-done="todo.isDone = $event"
      />
    </ul>
  </div>
</template>

<style>
body {
  background: #f5f7fa;
  margin: 0;
  padding: 20px;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  min-height: 100vh;
}

.todo-wrapper {
  max-width: 500px;
  margin: 0 auto;
  background: #ffffff;
  border-radius: 12px;
  padding: 30px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
  border: 1px solid #e9ecef;
}

.todo-wrapper h1 {
  color: #2c3e50;
  text-align: center;
  margin-bottom: 30px;
  font-size: 2.2rem;
  font-weight: 600;
}

.todo-wrapper p {
  text-align: center;
  color: #666;
  font-style: italic;
  font-size: 1.1rem;
  margin: 40px 0;
}

.todo-done {
  text-decoration: line-through;
  opacity: 0.6;
}

li {
  list-style: none;
  margin-bottom: 10px;
}

ul {
  padding: 0;
  margin-top: 30px;
}
</style>
