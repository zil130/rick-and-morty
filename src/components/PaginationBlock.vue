<script setup>
defineEmits(['prev', 'next']);

const props = defineProps({
  pages: {
    type: Object,
    required: true,
  },
  currentPage: {
    type: Number,
    required: true,
  }
});
</script>

<template>
  <div class="pagination">
    <button
      class="btn"
      @click="$emit('prev', currentPage - 1)"
      :disabled="!pages.prev"
    >Prev</button>
    <span>page {{ currentPage }} of {{ pages.pages }}</span>
    <button
      class="btn"
      @click="$emit('next', currentPage + 1)"
      :disabled="!pages.next"
    >Next</button>
  </div>
</template>

<style scoped>
.pagination {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 15px;
  margin-bottom: 15px;
}

.btn {
  padding: 5px 10px;
  cursor: pointer;
}

.btn:disabled {
  cursor: not-allowed;
}
</style>
