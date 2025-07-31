<!-- Composition APIの書き方 -->

<script setup>
import { ref } from 'vue'

const newTodoText = ref('')
const emit = defineEmits(['add-todo', 'clear-todo'])

function add() {
  if (!newTodoText.value) {
    alert('文字を入力してください')
    return
  }
  emit('add-todo', newTodoText.value)
  newTodoText.value = ''
}

function clear() {
  emit('clear-todo')
}
</script>

<template>
  <div class="input-container">
    <input
      type="text"
      v-model="newTodoText"
      class="todo-input"
      placeholder="新しいタスクを入力..."
    />
    <div class="button-group">
      <button @click="add" class="add-btn">
        <span>追加</span>
      </button>
      <button @click="clear" class="clear-btn">
        <span>完了済みを削除</span>
      </button>
    </div>
  </div>
</template>

<style>
.input-container {
  margin-bottom: 20px;
}

.todo-input {
  width: 100%;
  height: 45px;
  border: 2px solid #e9ecef;
  border-radius: 8px;
  padding: 0 15px;
  font-size: 16px;
  background: #ffffff;
  transition: border-color 0.2s ease;
  box-sizing: border-box;
  margin-bottom: 15px;
}

.todo-input:focus {
  outline: none;
  border-color: #007bff;
}

.button-group {
  display: flex;
  gap: 10px;
}

.add-btn,
.clear-btn {
  flex: 1;
  height: 45px;
  border: none;
  border-radius: 8px;
  font-size: 14px;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s ease;
}

.add-btn {
  background: #007bff;
  color: white;
}

.add-btn:hover {
  background: #0056b3;
  transform: translateY(-1px);
}

.clear-btn {
  background: #dc3545;
  color: white;
}

.clear-btn:hover {
  background: #c82333;
  transform: translateY(-1px);
}

.add-btn:active,
.clear-btn:active {
  transform: translateY(0);
}
</style>
