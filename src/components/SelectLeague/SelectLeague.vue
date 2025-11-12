<script setup>
const props = defineProps({
  selectedSport: String,
});
const emit = defineEmits(["update-sport"]);
</script>

<template>
  <select
    :value="props.selectedSport"
    @change="emit('update-sport', $event.target.value)"
    class="selectBox"
  >
    <option value="All">All</option>
    <option value="Soccer">Soccer</option>
    <option value="Motorsport">Motorsport</option>
    <option value="Basketball">Basketball</option>
    <option value="American Football">American Football</option>
    <option value="Ice Hockey">Ice Hockey</option>
  </select>
</template>

<style scoped>
@media (max-width: 480px) {
  .selectBox {
    width: 100%;
  }
  }
  @media (max-width: 300px) {
  .selectBox {
    width: 50%;
    margin-right: 15px;
  }
  }
</style>
