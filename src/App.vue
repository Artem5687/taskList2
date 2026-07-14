<script setup>
import { ref } from 'vue';

let taskList = ref([
  { text: 'Прочитать про переменные java.skript', done: false },
  { text: 'Дописать таск лист', done: false },
  { text: 'Прочитать про события во вьюждиес', done: false },
  { text: 'написать кнопки для создания и удаления задач', done: false },
  { text: 'раставить чек боксы чтобы можно отвечать задачи закрыте', done: false },
  { text: 'Прочитать про переменные java.skript', done: false },
  { text: 'Прочитать про переменные java.skript', done: false },
])

function toggleTaskState(task) { task.done = !task.done }
function deleteTask(index) { taskList.value.splice(index, 1) }

let newTask = ref('');

function addTask() {
  if (newTask.value == '') { return false }
  taskList.value.push({ text: newTask.value, done: false });
  newTask.value = '';
}
</script>

<template>
  <div class="container">
    <!-- Заголовок -->
    <div class="header">
      <h1>📋 Список задач</h1>
      <p class="subtitle">Организуй свои дела</p>
    </div>

    <!-- Статистика -->
    <div class="stats">
      <div class="stat-item">
        <span class="stat-number">{{ taskList.length }}</span>
        <span class="stat-label">Всего задач</span>
      </div>
      <div class="stat-item">
        <span class="stat-number">{{ taskList.filter(t => t.done).length }}</span>
        <span class="stat-label">Выполнено</span>
      </div>
      <div class="stat-item">
        <span class="stat-number">{{ taskList.filter(t => !t.done).length }}</span>
        <span class="stat-label">Осталось</span>
      </div>
    </div>

    <!-- Добавление задачи -->
    <div class="add-section">
      <h2>Новая пытка</h2>
      <div class="add-form">
        <input 
          class="add-input" 
          v-model="newTask" 
          placeholder="Введите задачу..." 
          @keyup.enter="addTask" 
        />
        <button class="add-button" @click="addTask"> Гроб</button>
      </div>
    </div>

    <!-- Список задач -->
    <div class="tasks-section">
      <h2>Мучения Троцкого</h2>
      
      <div v-if="taskList.length === 0" class="empty-state">
        <p>Ураааааааа ты выжил</p>
        <p class="empty-sub">надеюсь тебя убьют</p>
      </div>

      <div v-for="(item, index) in taskList" :key="index" 
        class="task-item"
        :class="{ 'task-item-done': item.done }"
      >
        <div class="task-content">
          <input class="task-checkbox" type="checkbox" v-model="item.done" />
          <p class="task-text" @click="toggleTaskState(item)">{{ item.text }}</p>
        </div>
        <button class="task-delete" @click="deleteTask(index)">🗑️</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 40px 20px;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background: #f8f9fa;
  min-height: 100vh;
}

/* Заголовок */
.header {
  text-align: center;
  margin-bottom: 40px;
  padding: 30px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  border-radius: 16px;
  color: white;
  box-shadow: 0 10px 30px rgba(102, 126, 234, 0.3);
}

.header h1 {
  font-size: 42px;
  font-weight: 700;
  margin-bottom: 8px;
}

.subtitle {
  font-size: 18px;
  opacity: 0.9;
}

/* Статистика */
.stats {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
  margin-bottom: 40px;
}

.stat-item {
  background: white;
  padding: 20px;
  border-radius: 12px;
  text-align: center;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.06);
  transition: transform 0.2s;
}

.stat-item:hover {
  transform: translateY(-4px);
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.1);
}

.stat-number {
  display: block;
  font-size: 32px;
  font-weight: 700;
  color: #2d3748;
}

.stat-label {
  font-size: 14px;
  color: #718096;
  margin-top: 4px;
}

/* Добавление задачи */
.add-section {
  background: white;
  padding: 24px;
  border-radius: 12px;
  margin-bottom: 32px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.06);
}

.add-section h2 {
  font-size: 20px;
  color: #2d3748;
  margin-bottom: 16px;
}

.add-form {
  display: flex;
  gap: 12px;
}

.add-input {
  flex: 1;
  padding: 12px 16px;
  border: 2px solid #e2e8f0;
  border-radius: 8px;
  font-size: 16px;
  transition: all 0.3s;
  outline: none;
}

.add-input:focus {
  border-color: #667eea;
  box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
}

.add-input::placeholder {
  color: #a0aec0;
}

.add-button {
  padding: 12px 24px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-size: 16px;
  font-weight: 600;
  transition: all 0.3s;
  white-space: nowrap;
}

.add-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(102, 126, 234, 0.4);
}

.add-button:active {
  transform: translateY(0);
}

/* Список задач */
.tasks-section {
  background: white;
  padding: 24px;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.06);
}

.tasks-section h2 {
  font-size: 20px;
  color: #2d3748;
  margin-bottom: 16px;
}

.task-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px 16px;
  margin-bottom: 8px;
  background: #f7fafc;
  border-radius: 8px;
  transition: all 0.3s;
  border-left: 4px solid transparent;
}

.task-item:hover {
  background: #edf2f7;
  transform: translateX(4px);
}

.task-item-done {
  background: #f0fff4;
  border-left-color: #48bb78;
  opacity: 0.7;
}

.task-item-done:hover {
  background: #e6fffa;
}

.task-content {
  display: flex;
  align-items: center;
  gap: 12px;
  flex: 1;
}

.task-checkbox {
  width: 20px;
  height: 20px;
  cursor: pointer;
  accent-color: #48bb78;
  flex-shrink: 0;
}

.task-text {
  flex: 1;
  margin: 0;
  font-size: 16px;
  color: #2d3748;
  cursor: pointer;
  padding: 4px 0;
  transition: color 0.3s;
}

.task-text:hover {
  color: #667eea;
}

.task-item-done .task-text {
  text-decoration: line-through;
  color: #a0aec0;
}

.task-delete {
  background: #fc8181;
  color: white;
  border: none;
  padding: 6px 12px;
  border-radius: 6px;
  cursor: pointer;
  font-size: 18px;
  transition: all 0.3s;
  flex-shrink: 0;
  opacity: 0.6;
}

.task-delete:hover {
  background: #f56565;
  opacity: 1;
  transform: scale(1.1);
}

/* Пустое состояние */
.empty-state {
  text-align: center;
  padding: 40px 20px;
}

.empty-state p {
  font-size: 20px;
  color: #2d3748;
  margin-bottom: 4px;
}

.empty-sub {
  font-size: 16px;
  color: #a0aec0;
}

/* Адаптивность */
@media (max-width: 600px) {
  .container {
    padding: 20px 16px;
  }

  .header h1 {
    font-size: 28px;
  }

  .stats {
    grid-template-columns: 1fr;
  }

  .add-form {
    flex-direction: column;
  }

  .add-button {
    width: 100%;
  }

  .task-item {
    padding: 10px 12px;
  }

  .task-text {
    font-size: 14px;
  }
}
</style>
