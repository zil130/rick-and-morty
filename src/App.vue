<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import HeaderBlock from './components/HeaderBlock.vue';
import FormSearch from './components/FormSearch.vue';
import CharacterList from './components/CharacterList.vue';
import PaginationBlock from './components/PaginationBlock.vue';
import './App.css';

const characters = ref([]);
const error = ref('');
const isLoading = ref(false);
const count = ref(0);
const pages = ref({});
const currentPage = ref(1);
const params = ref({
  name: '',
  status: '',
});

const fetchCharacters = async (url) => {
  isLoading.value = true;
  error.value = '';
  count.value = 0;
  try {
    const response = await axios.get(url);
    characters.value = response.data.results;
    count.value = response.data.info.count;
    pages.value = response.data.info;
  } catch(e) {
    console.error('Error fetching characters:', e.message);
    error.value = 'A loading error has occurred';
    characters.value = [];
  } finally {
    isLoading.value = false;
  }
};

const applyFilters = () => {
  currentPage.value = 1;
  const queryParams = Object.entries(params.value)
    .filter(([_, value]) => value !== '')
    .map(([key, value]) => `${key}=${encodeURIComponent(value)}`)
    .join('&');
  const url = `https://rickandmortyapi.com/api/character/${queryParams ? `?${queryParams}` : ''}`
  fetchCharacters(url);
};

const prev = (newPage) => {
  currentPage.value = newPage;
  fetchCharacters(pages.value.prev);
};

const next = (newPage) => {
  currentPage.value = newPage;
  fetchCharacters(pages.value.next);
};

onMounted(() => fetchCharacters('https://rickandmortyapi.com/api/character/'));
</script>

<template>
  <HeaderBlock :count="count" />
  <FormSearch
    v-model:name="params.name"
    v-model:status="params.status"
    @apply-filters="applyFilters"
    :isLoading="isLoading"
  />
  <CharacterList
    :isLoading="isLoading"
    :error="error"
    :characters="characters"
  />
  <PaginationBlock
    v-if="!error && !isLoading"
    :pages="pages"
    :currentPage = "currentPage"
    @prev="prev"
    @next="next"
  />
</template>

<style></style>
