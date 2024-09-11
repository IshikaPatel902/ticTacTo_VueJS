<template>
  <div>
    <NavBar @search="updateFilter" />
    <br/>
    <div class="container text-center">
      <!-- Batsman Section -->
      <section class="section batsman-section">
        <h1>Batsman</h1>
        <div class="row">
          <div class="col" v-for="player in filteredPlayers('batsman')" :key="player.name">
            <div class="card player-card animate__animated animate__fadeInUp">
              <img :src="getImageSrc(player.image)" class="card-img-top" alt="Player Image">
              <div class="card-body">
                <h5 class="card-title">{{ player.name }}</h5>
                <p class="card-text">Matches: {{ player.matches }}</p>
                <p class="card-text">Runs: {{ player.runs }}</p>
                <p class="card-text">50s/100s: {{ player['50s'] }}/{{ player['100s'] }}</p>
                <p class="card-text">Highest Score: {{ player.highest_score }}</p>
                <p class="card-text">Team Name: {{ player.team_name }}</p>
                <p class="card-text">Best Bowling Figures: {{ player.best_bowling_figures }}</p>
              </div>
            </div>
          </div>
        </div>
      </section>
      
      <!-- Bowler Section -->
      <section class="section bowler-section">
        <h1>Bowlers</h1>
        <div class="row">
          <div class="col" v-for="player in filteredPlayers('bowler')" :key="player.name">
            <div class="card player-card animate__animated animate__fadeInUp">
              <img :src="getImageSrc(player.image)" class="card-img-top" alt="Player Image">
              <div class="card-body">
                <h5 class="card-title">{{ player.name }}</h5>
                <p class="card-text">Matches: {{ player.matches }}</p>
                <p class="card-text">Runs: {{ player.runs }}</p>
                <p class="card-text">50s/100s: {{ player['50s'] }}/{{ player['100s'] }}</p>
                <p class="card-text">Highest Score: {{ player.highest_score }}</p>
                <p class="card-text">Team Name: {{ player.team_name }}</p>
                <p class="card-text">Best Bowling Figures: {{ player.best_bowling_figures }}</p>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- All Rounders Section -->
      <section class="section all-rounder-section">
        <h1>All Rounders</h1>
        <div class="row">
          <div class="col" v-for="player in filteredPlayers('all-rounder')" :key="player.name">
            <div class="card player-card animate__animated animate__fadeInUp">
              <img :src="getImageSrc(player.image)" class="card-img-top" alt="Player Image">
              <div class="card-body">
                <h5 class="card-title">{{ player.name }}</h5>
                <p class="card-text">Matches: {{ player.matches }}</p>
                <p class="card-text">Runs: {{ player.runs }}</p>
                <p class="card-text">50s/100s: {{ player['50s'] }}/{{ player['100s'] }}</p>
                <p class="card-text">Highest Score: {{ player.highest_score }}</p>
                <p class="card-text">Team Name: {{ player.team_name }}</p>
                <p class="card-text">Best Bowling Figures: {{ player.best_bowling_figures }}</p>
              </div>
            </div>
          </div>
        </div>
      </section>
    </div>
  </div>
</template>


<script>
import NavBar from './NavBar.vue'
import { playersData } from '../playersData.js'

export default {
  name: 'PlayersList',
  components: {
    NavBar
  },
  data() {
    return {
      players: playersData.originalPlayers,
      fallbackImage: require('@/assets/images/img.jpg'),
      searchQuery: '',
      selectedTeam: 'ALL'
    }
  },
  methods: {
    filteredPlayers(role) {
      return this.players.filter(player => {
        if (role === 'batsman' && player.role === 2) return this.matchesFilters(player);
        if (role === 'all-rounder' && player.role === 3) return this.matchesFilters(player);
        if (role === 'bowler' && player.role === 4) return this.matchesFilters(player);
        return false;
      });
    },
    matchesFilters(player) {
      return (this.selectedTeam === 'ALL' || player.team_name === this.selectedTeam) &&
             (player.name.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
              player.team_name.toLowerCase().includes(this.searchQuery.toLowerCase()));
    },
    getImageSrc(imageUrl) {
      return imageUrl ? imageUrl : this.fallbackImage;
    },
    updateFilter(filters) {
      this.searchQuery = filters.query;
      this.selectedTeam = filters.team;
    }
  }
}
</script>

<style scoped>
/* General styles for sections */
.section {
  margin-bottom: 2rem;
}

.section h1 {
  font-size: 2.5rem;
  margin-bottom: 1.5rem;
  color: #333;
  font-family: 'Arial', sans-serif;
  text-transform: uppercase;
  position: relative;
}

.section h1::after {
  content: "";
  display: block;
  height: 3px;
  background: #007bff;
  width: 60px;
  margin: 10px auto 0;
}

.player-card {
  border: 1px solid #e0e0e0;
  border-radius: 10px;
  overflow: hidden;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.player-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.card-img-top {
  width: 100%;
  height: 270px;
  border-bottom: 1px solid #e0e0e0;
}

.card-body {
  padding: 1.5rem;
}

.card-title {
  font-size: 1.25rem;
  margin-bottom: 1rem;
  color: #333;
}

.card-text {
  margin-bottom: 0.5rem;
  color: #555;
}

/* Animation styles */

/* Responsive adjustments */
@media (max-width: 767px) {
  .player-card {
    margin-bottom: 1rem;
  }
}

</style>
