<script setup>
const props = defineProps({
  filteredLeagues: Array,
  badges: Array
})
</script>

<template>
  <div class="leaguesBox">
    <div 
      v-for="league in props.filteredLeagues"
      :key="league.idLeague"
      @click="$emit('select-league',league.idLeague)"
      class="leagueCard"
    >
      <h1>{{ league.strLeague }}</h1>
      <h2>{{ league.strSport }}</h2>
      <h3>{{ league.strLeagueAlternate }}</h3>
    </div>
  </div>
</template>

<style scoped>
.leaguesBox {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 30px;
  
}
.leagueCard {
  width: 500px;
  height: 200px;
  border-radius: 15px;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
  padding: 15px;
  cursor: pointer;
}
</style>
