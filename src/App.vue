<script setup>
import { ref, computed, watch, onMounted } from "vue";
import Form from "./components/Form.vue";
import TaskItem from "./components/TaskItem.vue";

const tasks = ref([]);

onMounted(() => {
  const storedTasks = localStorage.getItem("tasks");
  if (storedTasks) {
    tasks.value = JSON.parse(storedTasks);
  } else {
    tasks.value = [];
  }
});

watch(
  tasks,
  (newValue) => {
    localStorage.setItem("tasks", JSON.stringify(newValue));
  },
  {
    deep: true
  }
);

// Добавление новой задачи
const taskName = ref("");

function handleInput(val) {
  taskName.value = val;
}

function addTask() {
  if (taskName.value.trim() === "") {
    return;
  }

  const newTask = {
    name: taskName.value.trim(),
    isCompleted: false
  };

  tasks.value.push(newTask);
  taskName.value = "";
}

// Обновление состояния задачи
function toggleTask(task) {
  task.isCompleted = !task.isCompleted;
}

// Удаление задачи
function deleteTask(task) {
  const idx = tasks.value.indexOf(task);
  if (idx !== -1) {
    tasks.value.splice(idx, 1);
  }
}

// Сортировка задач
const sortedTasks = computed(() => {
  return [...tasks.value].sort((a, b) => {
    return Number(!b.isCompleted) - Number(!a.isCompleted);
  });
});
</script>

<template>
  <div class="container">
    <div class="header">
      <h1 class="header-title">ToDoList App</h1>
    </div>
    <Form
      :taskname="taskName"
      :set-taskname="handleInput"
      :add-task="addTask"
    />
    <ul class="list">
      <TaskItem
        v-for="(task, index) in sortedTasks"
        :key="index"
        :toggle-task="() => toggleTask(task)"
        :delete-task="() => deleteTask(task)"
        :task="task"
      />
    </ul>
  </div>
</template>

<style>
.container {
  width: 960px;
  margin: 100px auto;
  border: 1px solid var(--border);
  border-radius: 36px;
  padding: 32px 48px;
}

.header-title {
  font-size: 32px;
  line-height: 40px;
  font-weight: 700;
  text-align: center;
}

.btn {
  padding: 8px 16px;
  border-radius: 8px;
  color: #fff;
  cursor: pointer;
  transition: 0.2s ease;
}

.btn-green {
  border: 1px solid var(--green);
  background: var(--green);
}

.btn-green:hover {
  background: #fff;
  color: var(--green);
}

.btn-red {
  border: 1px solid var(--red);
  background: var(--red);
}

.btn-red:hover {
  background: #fff;
  color: var(--red);
}

.list {
  display: flex;
  flex-direction: column;
  gap: 16px;
}
</style>
