<template>
  <div id="app">
    <GameBoard ref="gameBoard" />
    <button @click="resetGame">Reset Game</button>
    <p v-if="winner">Winner: {{ winner }}</p>
  </div>
</template>

<script>
import GameBoard from './components/GameBoard.vue';

export default {
  components: {
    GameBoard,
  },
  computed: {
    winner() {
      return this.$refs.gameBoard ? this.$refs.gameBoard.winner : null;
    },
  },
  methods: {
    resetGame() {
      if (this.$refs.gameBoard) {
        this.$refs.gameBoard.resetGame();
      }
    },
  },
};
</script>

<style>
#app {
  text-align: center;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
  margin-top: 60px;
}
button {
  margin-top: 20px;
}
</style>
