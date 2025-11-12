<script setup>
import { ref, onMounted, computed } from "vue";
import axios from "axios";
import SearchBox from "../SearchBox/SearchBox.vue";
import LeagueList from "../LeagueList/LeagueList.vue";
import LeagueBadges from "../LeagueBadges/LeagueBadges.vue";
import SelectLeague from "../SelectLeague/SelectLeague.vue";

const leagues = ref([]);
const badgeUrl = ref(null);
const search = ref("");
const selectedSport = ref("All");

onMounted(async () => {
  try {
    const res = await axios.get("https://www.thesportsdb.com/api/v1/json/3/all_leagues.php");
    leagues.value = res.data.leagues;
  } catch (e) {
    console.error("Error loading leagues:", e);
  }
});

async function getBadges(idLeague) {
  const cacheKey = `league_badge_${idLeague}`; 
  const cached = localStorage.getItem(cacheKey);
  if (cached) {
    badgeUrl.value = JSON.parse(cached);
    return;
  }
  try {
    const res = await axios.get(
      `https://www.thesportsdb.com/api/v1/json/3/lookupleague.php?id=${idLeague}`
    );
    const badge = res.data.leagues?.[0]?.strBadge || null;
    badgeUrl.value = badge;
    if (badge) localStorage.setItem(cacheKey, JSON.stringify(badge));
  } catch (e) {
    console.error("Error loading badges:", e);
  }
}

const filteredFinal = computed(() =>
  leagues.value.filter((league) => {
    const sportMatch =
      selectedSport.value === "All" || league.strSport === selectedSport.value;
    const nameMatch = !search.value.toLowerCase().trim() || league.strLeague.toLowerCase().startsWith(search.value.toLowerCase().trim());
    return sportMatch && nameMatch;
  })
);

function updateSearch(v) { search.value = v; }
</script>

<template>
  <div class="searchBox">
    <SearchBox :search="search" @update-search="updateSearch" />
    <SelectLeague :selectedSport="selectedSport" @update-sport="selectedSport = $event" />
  </div>

  <LeagueList :filteredLeagues="filteredFinal" @select-league="getBadges" />

 
  <LeagueBadges :url="badgeUrl" @close="badgeUrl = null" />
</template>

<style scoped>
.searchBox {
  display: flex;
  justify-content: space-around;
  align-items: center;
}
@media (max-width: 780px) {
  .searchBox{
    display: flex;
    flex-direction: column;
  }
}
</style>
