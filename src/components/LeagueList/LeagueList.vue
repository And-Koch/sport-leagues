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
  display: flex;
  flex-direction: column;
  gap: 25px;
  width: 500px;
  height: 200px;
  border-radius: 15px;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
  padding: 15px;
  cursor: pointer;
}
@media (max-width: 780px) {

  .leagueCard h1 {
    font-size: 1.1rem;
  }
  .leagueCard h2 {
    font-size: 0.95rem;
  }
  .leagueCard h3 {
    font-size: 0.85rem;
  }
}
@media (max-width: 480px) {
  .leaguesBox {
    grid-template-columns: 1fr;
  }
  .leagueCard {
    margin: 10px;
    padding: 12px;
  }
}
@media (max-width: 300px) {
 
    .leaguesBox {
    grid-template-columns: 1fr;
    width: 270px;
    margin: auto;
  }
  .leagueCard {
    padding: 12px;
  }
}
</style>
