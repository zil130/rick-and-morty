<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import HeaderBlock from './components/HeaderBlock.vue';
import CharacterCard from './components/CharacterCard.vue';
import './App.css';

const characters = ref([]);
const error = ref('');
const isLoading = ref(false);
const count = ref(0);

const fetchCharacters = async () => {
  isLoading.value = true;
  error.value = '';
  count.value = 0;
  try {
    const response = await axios.get('https://rickandmortyapi.com/api/character');
    characters.value = response.data.results;
    count.value = response.data.info.count;
  } catch(e) {
    console.error('Error fetching characters:', e.message);
    error.value = 'A loading error has occurred. Try refreshing the page';
  } finally {
    isLoading.value = false;
  }
};

onMounted(fetchCharacters);
</script>

<template>
  <HeaderBlock :count="count" />
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

<style>
.cards {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
}
</style>
