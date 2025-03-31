<script setup>
import { ref } from "vue";

const count = ref(5);

function inc() {
  count.value++;
}

function dec() {
  count.value--;
}
</script>

<template>
  <div class="counter">
    <button class="btn" @click="dec">-</button>
    <span class="number text">{{ count }}</span>
    <button class="btn" @click="inc">+</button>
  </div>
</template>

<style scoped>
.counter {
  border: 1px solid #cdcdcd;
  padding: 16px;
  border-radius: 12px;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 32px;
}

.btn {
  width: 48px;
  aspect-ratio: 1/1;
  border: 1px solid #cdcdcd;
  border-radius: 100%;
  font-size: 20px;
  font-weight: 700;
  cursor: pointer;
}

.number {
  font-size: 28px;
  font-weight: 500;
}

.text {
  color: #ff8000;
}
</style>
