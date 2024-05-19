<script setup>
defineEmits(['apply-filters']);

const name = defineModel('name');
const status = defineModel('status');
const props = defineProps({
  isLoading: Boolean,
  required: true,
});
</script>

<template>
  <form
    class="form"
    @submit.prevent="$emit('apply-filters')"
  >
    <label>Filter by name:
      <input class="input" type="text" v-model.trim="name" />
    </label>
    <label>Filter by status:
      <select class="select" v-model="status">
        <option value="">All</option>
        <option value="alive">Alive</option>
        <option value="dead">Dead</option>
        <option value="unknown">Unknown</option>
      </select>
    </label>
    <button
      class="btn"
      :disabled="isLoading"
    >Apply</button>
  </form>
</template>

<style scoped>
.form {
  display: flex;
  justify-content: center;
  gap: 15px;
}

.input {
  padding: 5px 10px;
}

.select {
  padding: 5px 10px;
  cursor: pointer;
}

.btn {
  padding: 5px 10px;
  cursor: pointer;
}
</style>
