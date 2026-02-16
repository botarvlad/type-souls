<template>
  <div class="word-container">
    <div class="word">
      <p class="completed">Char input:{{ props.charInput.char }}</p>
      <p class="completed">Word:{{ word }}</p>
      <p class="completed">Completed:{{ completed }}</p>
      <p class="remaining">Remaining:{{ remaining }}</p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed, ref, watch } from 'vue';
import wordsData from '@/data/words.json'

interface WordsFile {
  words: string[]
}

const props = defineProps<{
  charInput: { char: string; id: number }
}>();

const data  = wordsData as WordsFile;

const getRandomWord = (): string => {
  const randomIndex = Math.floor(Math.random() * data.words.length);
  return data.words[randomIndex] || '';
}

const word = ref<string>(getRandomWord())
const progress = ref<string>('')


const pickRandomWord = () => {
  word.value = getRandomWord();
}

watch(
  () => props.charInput.id,
  () => {
    const newChar = props.charInput.char;
    if (!newChar) return;
    
    const expectedChar = word.value[progress.value.length];

    if (newChar === expectedChar) {
      progress.value += newChar;

      if (progress.value === word.value) {
        pickRandomWord();
        reset();
      }
    } else {
      reset()
    }
  }
)

const reset = (): void => {
  progress.value = '';
}

const completed = computed(() => progress.value)

const remaining = computed(() => word.value.slice(progress.value.length))
</script>

<style scoped></style>
