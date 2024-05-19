<script setup>
import CharacterCard from './CharacterCard.vue';

const props = defineProps({
  isLoading: {
    type: Boolean,
    required: true,
  },
  error: {
    type: String,
    required: true,
  },
  characters: {
    type: Object,
    required: true,
  }
});
</script>

<template>
  <div class="cards">
    <p v-if="error">{{ error }}</p>
    <p v-if="isLoading">Loading...</p>
    <CharacterCard
      v-else
      v-for="character in characters"
      :character="character"
      :key="character.id"
    />
  </div>
</template>

<style scoped>
.cards {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
}
</style>
