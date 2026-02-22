<template>
  <div class="game">
    <BarEnemy :char-input="charInput" />
    <BarEnemy :char-input="charInput" />
    <BarEnemy :char-input="charInput" />
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue';
import BarEnemy from './components/BarEnemy.vue';

const charInput = ref<{ char: string; id: number }>({ char: '', id: 0 });

const handleKey = (event: KeyboardEvent): void => {
  if (event.key.length === 1) {
    const ch = event.key.toLowerCase();
    if (/^[a-z]$/.test(ch)) {
      charInput.value = { char: ch, id: charInput.value.id + 1 };
    }
  }

  event.preventDefault();
};

// listen on window so user can type "in the air"
onMounted(() => {
  window.addEventListener('keydown', handleKey);
});

onBeforeUnmount(() => {
  window.removeEventListener('keydown', handleKey);
});
</script>

<style scoped>
.game {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 16px;
}
</style>
