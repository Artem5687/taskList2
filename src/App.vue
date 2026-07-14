<script setup>
import { ref } from 'vue';

let taskList = ref([
  { text: 'Прочитать про переменные java.skript',                    done: false },
  { text: 'Дописать таск лист',                                      done: false },
  { text: 'Прочитать про события во вьюждиес',                       done: false },
  { text: 'написать кнопки для создания и удаления задач',           done: false },
  { text: 'раставить чек боксы чтобы можно отвечать задачи закрыте', done: false },
  { text: 'Прочитать про переменные java.skript',                    done: false },
  { text: 'Прочитать про переменные java.skript',                    done: false },
])

function toggleTaskState (task) { task.done = !task.done }
function deleteTask (index) { taskList.value.splice(index, 1) }

let newTask = ref('');

function addTask() {
  if (newTask.value == '') { return false }
  
  taskList.value.push({ text: newTask.value, done: false });
  newTask.value = '';
}
</script>

<template>
  <section class="todoList">
    <!-- Список задач -->
    <div v-for="(item, index) in taskList" :key="index" 
      class="todoList--item"
      :class="{ 'todoList--item-done': item.done == true }"
    >
      <input class="todoList--itemCheck" type="checkbox" v-model="item.done" />

      <p class="todoList--itemText" @click="toggleTaskState(item)">{{ item.text }}</p>

      <button class="todoList--itemButton" @click="deleteTask(index)"> 🗑🚮 </button>
    </div>

    <!-- Добавление задачи -->
    <div>
      <input v-model="newTask" placeholder="Новая задача" @keyup.enter="addTask" />
      <button @click="addTask"> голый пудж</button>
    </div>
  </section>
</template>

<style scoped>
.todoList {
  max-width: 700px;
  margin: 0 auto;
  padding: 30px 20px;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.todoList--item {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 12px 16px;
  margin-bottom: 8px;
  background: #f8f9fa;
  border-radius: 8px;
  transition: all 0.3s ease;
  border: 1px solid #e9ecef;
}

.todoList--item:hover {
  background: #f1f3f5;
  border-color: #dee2e6;
  transform: translateX(4px);
}

.todoList--item-done {
  background: #e8f5e9;
  border-color: #a5d6a7;
  opacity: 0.8;
}

.todoList--item-done:hover {
  background: #c8e6c9;
}

.todoList--itemCheck {
  width: 20px;
  height: 20px;
  cursor: pointer;
  accent-color: #4CAF50;
  flex-shrink: 0;
}

.todoList--itemCheck:hover {
  transform: scale(1.1);
}

.todoList--itemText {
  flex: 1;
  margin: 0;
  font-size: 16px;
  color: #212529;
  cursor: pointer;
  padding: 4px 0;
  transition: color 0.3s ease;
}

.todoList--itemText:hover {
  color: #0d6efd;
}

.todoList--item-done .todoList--itemText {
  text-decoration: line-through;
  color: #6c757d;
}

.todoList--itemButton {
  background: #dc3545;
  color: white;
  border: none;
  padding: 8px 14px;
  border-radius: 6px;
  cursor: pointer;
  font-size: 16px;
  transition: all 0.3s ease;
  flex-shrink: 0;
}

.todoList--itemButton:hover {
  background: #c82333;
  transform: scale(1.05);
}

.todoList--itemButton:active {
  transform: scale(0.95);
}

.todoList--add {
  display: flex;
  gap: 12px;
  margin-top: 30px;
  padding-top: 20px;
  border-top: 2px solid #dee2e6;
}

.todoList--addInput {
  flex: 1;
  padding: 12px 16px;
  border: 2px solid #dee2e6;
  border-radius: 8px;
  font-size: 16px;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  transition: all 0.3s ease;
  outline: none;
}

.todoList--addInput:focus {
  border-color: #4CAF50;
  box-shadow: 0 0 0 3px rgba(76, 175, 80, 0.2);
}

.todoList--addInput::placeholder {
  color: #adb5bd;
}

.todoList--addButton {
  padding: 12px 28px;
  background: #4CAF50;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-size: 16px;
  font-weight: 600;
  transition: all 0.3s ease;
  white-space: nowrap;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.todoList--addButton:hover {
  background: #43a047;
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(76, 175, 80, 0.3);
}

.todoList--addButton:active {
  transform: translateY(0);
  box-shadow: none;
}
</style>