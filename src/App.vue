<template>
  <div class="words-container">
    <Word :char-input="charInput" />
  </div>

  <input
    ref="inputRef"
    @keydown="handleKey"
  />

  <p>Last typed character: {{ charInput.char }}</p>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import Word from './components/Word.vue';

const charInput = ref<{ char: string; id: number}>({ char: '', id: 0 });

const handleKey = (event: KeyboardEvent): void => {
  if (event.key.length === 1) {
    charInput.value = { char: event.key, id: charInput.value.id + 1 };
  }

  event.preventDefault()
}
</script>

<style scoped>
.words-container {
  display: flex;
  gap: 20px;
}
</style>
