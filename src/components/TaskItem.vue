<script setup>
defineProps({
  task: Object,
  toggleTask: Function,
  deleteTask: Function
});
</script>

<template>
  <li class="task" :class="{ opacity: task.isCompleted }">
    <div class="task-part">
      <div class="toggle-out" v-on:click="toggleTask">
        <div class="toggle-in" v-if="task.isCompleted"></div>
      </div>
      <p class="task-name" :class="{ done: task.isCompleted }">
        {{ task.name }}
      </p>
    </div>
    <div class="task-part">
      <button
        class="btn btn-red"
        @click="deleteTask"
        :disabled="task.isCompleted"
      >
        Удалить
      </button>
    </div>
  </li>
</template>

<style scoped>
.task {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.task:not(:first-child) {
  padding-top: 16px;
  border-top: 1px solid var(--border);
}

.task-part:first-child {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  gap: 24px;
}

.toggle-out {
  width: 32px;
  aspect-ratio: 1/1;
  border: 2px solid var(--green);
  display: flex;
  justify-content: center;
  align-items: center;
}

.toggle-in {
  width: 16px;
  aspect-ratio: 1/1;
  background: var(--green);
}

.task-name {
  font-size: 18px;
}

.done {
  color: var(--green);
  text-decoration: line-through;
  font-weight: 700;
}

.opacity {
  opacity: 0.5;
}
</style>
