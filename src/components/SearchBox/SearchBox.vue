<script setup>
const props = defineProps({
  search: String,
});

const emit = defineEmits(["update-search"]);
</script>

<template>
  <div class="searchBox">
    <input
      type="text"
      :value="props.search"
      @input="emit('update-search', $event.target.value)"
      placeholder="Search leagues..."
    />
  </div>
</template>

<style scoped>
.searchBox {
  margin: 20px;
}
input {
  width: 200px;
  padding: 5px;
  border-radius: 15px;
  border: 1px solid gray;
}
</style>
