<script setup>
defineProps({
  taskname: String,
  setTaskname: Function,
  addTask: Function
});
</script>

<template>
  <form class="form" @submit.prevent="addTask">
    <input
      type="text"
      class="form-input"
      placeholder="Введите название задачи"
      :value="taskname"
      v-on:input="(e) => setTaskname(e.target.value)"
    />
    <button type="submit" class="btn btn-green">Добавить</button>
  </form>
</template>

<style scoped>
.form {
  margin: 24px 0 36px;
  display: flex;
  align-items: center;
  gap: 12px;
}

.form-input {
  flex: 1 0;
  outline: 2px solid var(--green);
  padding: 8px 16px;
  border-radius: 12px;
}
</style>
