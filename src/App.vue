<script setup>
import Counter from "./components/Counter.vue";
</script>

<template>
  <div class="container">
    <h1 class="title text">Counters App</h1>
    <div class="grid">
      <Counter />
      <Counter />
      <Counter />
      <Counter />
      <Counter />
    </div>
  </div>
</template>

<style scoped>
.container {
  width: 1200px;
  margin: 100px auto;
}

.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 24px 40px;
}

.title {
  font-size: 32px;
  line-height: 40px;
  font-weight: 700;
  margin-bottom: 40px;
}
</style>
