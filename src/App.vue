<template>
  <section class="quoridor">
    <h1 class="quoridor__title">QUORIDOR</h1>
    <p class="quoridor__current-turn">
      Turno actual: {{ currentPlayer === 1 ? 'Jugador 1 (Rojo)' : 'Jugador 2 (Azul)' }}
    </p>
    <p v-if="winner" class="quoridor__winner">¡{{ winner }} ha ganado!</p>
    <board
      :board="board"
      :player1="player1"
      :player2="player2"
      :obstacles="obstacles"
      @cell-click="handleCellClick"
    />
    <button @click="restart" class="quoridor__button">Reiniciar Juego</button>
    <footer class="quoridor__footer">
      <p>Realizado por<br>
      Cristian Javier Rodríguez Cárdenas<br>
      Frans Sebastian Villamizar Maldonado</p>
    </footer>
  </section>
</template>

<script>
import Board from './components/organisms/Board.vue';

export default {
  components: {
    Board
  },
  data() {
    return {
      board: this.createBoard(),
      player1: { x: 4, y: 0, color: 'var(--player1-color)' },
      player2: { x: 4, y: 8, color: 'var(--player2-color)' },
      currentPlayer: 1,
      obstacles: [],
      winner: null
    }
  },
  methods: {
    createBoard() {
      return Array(9).fill().map(() => Array(9).fill(null));
    },
    restart() {
      this.board = this.createBoard();
      this.player1 = { x: 4, y: 0, color: 'var(--player1-color)' };
      this.player2 = { x: 4, y: 8, color: 'var(--player2-color)' };
      this.currentPlayer = 1;
      this.obstacles = [];
      this.winner = null;
    },
    handleCellClick(i, j) {
      if (this.winner) return;

      const currentPlayer = this.currentPlayer === 1 ? this.player1 : this.player2;

      if (this.isValidMove(i, j)) {
        currentPlayer.x = j;
        currentPlayer.y = i;
        this.checkForWinner();
        this.currentPlayer = this.currentPlayer === 1 ? 2 : 1;
      } else if (!this.isPlayer1(i, j) && !this.isPlayer2(i, j) && !this.isObstacle(i, j)) {
        this.placeObstacle(i, j);
        this.currentPlayer = this.currentPlayer === 1 ? 2 : 1;
      }
    },
    isValidMove(i, j) {
      const currentPlayer = this.currentPlayer === 1 ? this.player1 : this.player2;
      const dx = Math.abs(j - currentPlayer.x);
      const dy = Math.abs(i - currentPlayer.y);
      if ((dx === 1 && dy === 0) || (dx === 0 && dy === 1)) {
        return !this.isObstacle(i, j);
      }
      return false;
    },
    placeObstacle(i, j) {
      this.obstacles.push({ x: j, y: i });
    },
    isPlayer1(i, j) {
      return this.player1.x === j && this.player1.y === i;
    },
    isPlayer2(i, j) {
      return this.player2.x === j && this.player2.y === i;
    },
    isObstacle(i, j) {
      return this.obstacles.some(obstacle => obstacle.x === j && obstacle.y === i);
    },
    checkForWinner() {
      if (this.player1.y === 8) {
        this.winner = 'Jugador 1 (Rojo)';
      } else if (this.player2.y === 0) {
        this.winner = 'Jugador 2 (Azul)';
      }
    }
  }
}
</script>

<style scoped>
/* Estilos específicos de App.vue */
.quoridor {
  text-align: center;
  padding: 20px;
  background-color: var(--background-color);
}

.quoridor__title {
  margin-bottom: 20px;
  font-size: 2.5rem;
  color: var(--primary-color);
}

.quoridor__current-turn {
  font-weight: bold;
  font-size: 1.2rem;
  margin-bottom: 10px;
  color: var(--primary-color);
}

.quoridor__winner {
  color: green;
  font-size: 1.5rem;
  margin-bottom: 10px;
}

.quoridor__button {
  display: inline-block;
  margin: 20px auto;
  padding: 10px 20px;
  background-color: var(--primary-color);
  color: white;
  border: none;
  cursor: pointer;
  border-radius: 5px;
  font-size: 1rem;
  transition: background-color 0.3s;
}

.quoridor__button:hover {
  background-color: var(--primary-hover-color);
}

.quoridor__footer {
  margin-top: 20px;
  font-size: 0.9rem;
  color: gray;
}
</style>