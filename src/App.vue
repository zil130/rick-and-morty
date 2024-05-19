<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import HeaderBlock from './components/HeaderBlock.vue';
import CharacterList from './components/CharacterList.vue';
import './App.css';
import FormSearch from './components/FormSearch.vue';

const characters = ref([]);
const error = ref('');
const isLoading = ref(false);
const count = ref(0);
const params = ref({
  name: '',
  status: '',
});

const fetchCharacters = async () => {
  isLoading.value = true;
  error.value = '';
  count.value = 0;
  try {
    const queryParams = Object.entries(params.value)
      .filter(([_, value]) => value !== '')
      .map(([key, value]) => `${key}=${encodeURIComponent(value)}`)
      .join('&');
    const url = `https://rickandmortyapi.com/api/character/${queryParams ? `?${queryParams}` : ''}`;
    const response = await axios.get(url);
    characters.value = response.data.results;
    count.value = response.data.info.count;
  } catch(e) {
    console.error('Error fetching characters:', e.message);
    error.value = 'A loading error has occurred';
    characters.value = [];
  } finally {
    isLoading.value = false;
  }
};

onMounted(fetchCharacters);
</script>

<template>
  <HeaderBlock :count="count" />
  <FormSearch
    v-model:name="params.name"
    v-model:status="params.status"
    @apply-filters="fetchCharacters"
    :isLoading="isLoading"
  />
  <CharacterList
    :isLoading="isLoading"
    :error="error"
    :characters="characters"
  />
</template>

<style></style>
