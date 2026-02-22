<template>
  <div class="bar-enemy">
    <FillingBar :fill-value="fillBar" />
    <WordComponent :char-input="charInput" @word-completed="onWordCompleted" />
  </div>
</template>

<script setup lang="ts">
import { onBeforeUnmount, onMounted, ref } from 'vue';
import FillingBar from './FillingBar.vue';
import WordComponent from './WordComponent.vue';

const props = defineProps<{
  charInput: { char: string; id: number };
}>();

const fillBar = ref<number>(0);
let intervalId: ReturnType<typeof setInterval> | null = null;

const onWordCompleted = () => {
  removeFilling();
};

const startFilling = () => {
  if (intervalId) return; // already running
  intervalId = setInterval(() => {
    if (fillBar.value < 100) {
      fillBar.value += 1;
    } else {
      return;
    }
  }, 500); // adjust speed here (ms per increment)
};

const stopFilling = () => {
  if (intervalId) {
    clearInterval(intervalId);
    intervalId = null;
  }
};

const removeFilling = () => {
  if (fillBar.value - 5 < 0) {
    fillBar.value = 0;
  } else {
    fillBar.value -= 5;
  }
};

onMounted(() => {
  startFilling();
});

onBeforeUnmount(() => {
  stopFilling();
});
</script>

<style scoped lang="scss">
.bar-enemy {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 8px;
  width: 160px;
}
</style>
