<!-- Composition APIの書き方 -->

<script setup>
const props = defineProps(['todo'])
const emit = defineEmits(['update-done'])

function toggleDone() {
  emit('update-done', !props.todo.isDone)
}
</script>

<template>
  <li class="todo-item">
    <label class="todo-label">
      <input type="checkbox" :checked="todo.isDone" @change="toggleDone" class="todo-checkbox" />
      <span class="checkmark"></span>
      <span :class="['todo-text', { 'todo-done': todo.isDone }]">
        {{ todo.text }}
      </span>
    </label>
  </li>
</template>

<style>
.todo-item {
  border-radius: 8px;
  padding: 15px;
  margin-bottom: 8px;
  border: 1px solid #e9ecef;
  transition: all 0.2s ease;
}

.todo-item:hover {
  border-color: #007bff;
  box-shadow: 0 2px 8px rgba(0, 123, 255, 0.1);
}

.todo-label {
  display: flex;
  align-items: center;
  cursor: pointer;
  user-select: none;
}

.todo-checkbox {
  display: none;
}

.checkmark {
  height: 18px;
  width: 18px;
  background: #ffffff;
  border: 2px solid #dee2e6;
  border-radius: 4px;
  margin-right: 12px;
  position: relative;
  transition: all 0.2s ease;
  flex-shrink: 0;
}

.todo-checkbox:checked ~ .checkmark {
  background: #007bff;
  border-color: #007bff;
}

.checkmark:after {
  content: '';
  position: absolute;
  display: none;
  left: 5px;
  top: 1px;
  width: 3px;
  height: 8px;
  border: solid white;
  border-width: 0 2px 2px 0;
  transform: rotate(45deg);
}

.todo-checkbox:checked ~ .checkmark:after {
  display: block;
}

.todo-text {
  flex: 1;
  font-size: 16px;
  color: #333;
  transition: all 0.3s ease;
}

.todo-text.todo-done {
  text-decoration: line-through;
  color: #999;
}
</style>
