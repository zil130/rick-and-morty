<script setup>
const props = defineProps({
  count: Number,
  required: true,
});
</script>

<template>
  <header class="header">
    <h1>Rick and Morty</h1>
    <h2>{{ count }} characters found</h2>
  </header>
</template>

<style scoped>
.header {
  display: flex;
  align-items: center;
  flex-direction: column;
}
</style>
