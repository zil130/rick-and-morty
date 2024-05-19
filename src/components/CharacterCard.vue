<script setup>
const props = defineProps({
  character: Object,
  required: true,
});
</script>

<template>
  <div class="card">
    <div class="img-block">
      <img class="img" :src="character.image" :alt="character.name">
    </div>
    <div class="info">
      <div class="section">
        <h2>{{ character.name }}</h2>
        <span>{{ character.status }} - {{ character.species }}</span>
      </div>
      <div class="section">
        <span>Last known location:</span>
        <span>{{ character.location.name }}</span>
      </div>
      <div class="section">
        <span>First seen in:</span>
        <span>{{ character.origin.name }}</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.card {
  width: 600px;
  height: 220px;
  margin: 0.75rem;
  display: flex;
  overflow: hidden;
  border: 2px solid grey;
  border-top: none;
  border-right: none;
  border-top-left-radius: 10px;
  border-bottom-left-radius: 10px;
}

.img-block {
  flex: 2 1 0%;
  width: 100%;
}

.img {
  width: 100%;
  height: 100%;
  margin: 0px;
  opacity: 1;
  transition: opacity 0.5s ease 0s;
  object-position: center center;
  object-fit: cover;
}

.info {
  flex: 3 1 0%;
  position: relative;
  padding: 0.75rem;
  display: flex;
  flex-direction: column;
}

.section {
  flex: 1 1 0%;
  display: flex;
  flex-direction: column;
  -webkit-box-pack: center;
  justify-content: center;
}
</style>
