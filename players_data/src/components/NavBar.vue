<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
    <div class="container-fluid">
      <a class="navbar-brand" href="#">Sportz Interactive</a>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <select class="form-select" name="team" id="team" @change="onTeamChange">
              <option value="ALL">ALL</option>
              <option value="India">IND</option>
              <option value="Pakistan">PAK</option>
              <option value="Australia">AUS</option>
              <option value="England">ENG</option>
            </select>
          </li>
        </ul>
        <form class="d-flex" role="search">
          <input class="form-control me-2" type="search" placeholder="Search" id="searchInput" v-model="searchQuery">
          <button class="btn btn-outline-light" type="button" @click="searchPlayers">Search</button>
        </form>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'NavBar',
  data() {
    return {
      searchQuery: '',
      selectedTeam: 'ALL'
    }
  },
  methods: {
    searchPlayers() {
      this.$emit('search', { query: this.searchQuery, team: this.selectedTeam });
    },
    onTeamChange(event) {
      this.selectedTeam = event.target.value;
    }
  }
}
</script>

<style scoped>
.navbar {
  background-color: #343a40; /* Dark background */
}
.navbar-brand {
  color: #ffffff; /* Light text color */
}
.navbar-light .navbar-toggler-icon {
  background-image: url('data:image/svg+xml,...'); /* Toggler icon color if needed */
}
.form-control {
  background-color: #495057; /* Dark background for input */
  color: #ffffff; /* Light text color for input */
}
.form-control::placeholder {
  color: #ced4da; /* Placeholder text color */
}
.btn-outline-light {
  color: #ffffff; /* Button text color */
  border-color: #ffffff; /* Button border color */
}
.btn-outline-light:hover {
  background-color: #ffffff; /* Button background color on hover */
  color: #343a40; /* Button text color on hover */
}
</style>
