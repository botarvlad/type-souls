<template>
  <div class="filling-bar-container">
    <div class="filling-bar-container__progess" :style="{ height: fillValue + '%' }"></div>
  </div>
</template>

<script setup lang="ts">
const props = defineProps<{
  fillValue: number;
}>();
</script>

<style scoped lang="scss">
.filling-bar-container {
  height: 400px;
  width: 30px;
  border: 2px solid black;
  rotate: 180deg;
  border-top-right-radius: 20px;
  border-top-left-radius: 20px;
  border-bottom-left-radius: 5px;
  border-bottom-right-radius: 5px;
  overflow: hidden;

  &__progess {
    background-color: rgb(35, 178, 73);
    width: 30px;
  }
}
</style>
