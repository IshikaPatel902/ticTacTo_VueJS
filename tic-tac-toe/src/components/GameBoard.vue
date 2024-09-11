<template>
  <div class="game-board">
    <div
      v-for="(cell, index) in board"
      :key="index"
      :class="['cell', cell]"
      @click="makeMove(index)"
    >
      {{ cell }}
    </div>
    <div v-if="winner" class="result-message">
      <p v-if="winner === 'Draw'">It's a Draw!</p>
      <p v-else>Winner: {{ winner }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      board: Array(9).fill(null),
      xIsNext: true,
      winner: null,
    };
  },
  methods: {
    makeMove(index) {
      if (this.board[index] || this.winner) return;
      this.$set(this.board, index, this.xIsNext ? 'X' : 'O');
      this.xIsNext = !this.xIsNext;
      this.checkWinner();
    },
    checkWinner() {
      const lines = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
      ];
      for (const [a, b, c] of lines) {
        if (this.board[a] && this.board[a] === this.board[b] && this.board[a] === this.board[c]) {
          this.winner = this.board[a];
          return;
        }
      }
      if (!this.board.includes(null)) {
        this.winner = 'Draw';
      }
    },
    resetGame() {
      this.board = Array(9).fill(null);
      this.xIsNext = true;
      this.winner = null;
    },
  },
};
</script>

<style scoped>
.game-board {
  display: grid;
  grid-template-columns: repeat(3, 100px);
  gap: 5px;
  justify-content: center;
  align-items: center;
  /* background-color: #000000; */
}
.cell {
  width: 100px;
  height: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 24px;
  background-color: #f0f0f0;
  cursor: pointer;
}
.cell:hover {
  background-color: #e0e0e0;
}
.cell.X {
  color: #ff0000; /* Neon red for X */
}

.cell.O {
  color: #009d18; /* Neon green for O */
}
.result-message {
  margin-top: 20px;
  font-size: 18px;
  font-weight: bold;
}
</style>
