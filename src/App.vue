<template>
  <AppHeader />
  <div id="app" class="game">
    <div class="board">
      <div v-for="(cell, index) in board" :key="index" class="cell" :class="{ 'cell-x': cell === 'X', 'cell-o': cell === 'O' }" @click="makeMove(index)">
        {{ cell }}
      </div>
    </div>
    <div v-if="winner" class="winner">
      <p>{{ winnerMessage }}</p>
      <button class="reset_Game" @click="resetGame">Reiniciar Juego</button>
    </div>
  </div>
  <AppFooter />
</template>

<script>
import { ref, computed } from "vue";
import AppHeader from './components/Header.vue';
import AppFooter from './components/Footer.vue';


export default {
  name: "TicTacToe",
  components: {
    AppHeader,
    AppFooter,
  },
  setup() {
    const board = ref(Array(9).fill(null));
    const currentPlayer = ref("X");
    const winner = ref(null);

    const winnerMessage = computed(() => {
      if (winner.value === 'Empate'){
        return "¡Empate!";
      }else{
        return `¡${winner.value} gana!`;
      }
    });

    const winningCombinations = [
      [0, 1, 2],
      [3, 4, 5],
      [6, 7, 8],
      [0, 3, 6],
      [1, 4, 7],
      [2, 5, 8],
      [0, 4, 8],
      [2, 4, 6],
    ];

    const checkWinner = () => {
      for (const combination of winningCombinations) {
        const [a, b, c] = combination;
        if (
          board.value[a] &&
          board.value[a] === board.value[b] &&
          board.value[a] === board.value[c]
        ) {
          winner.value = board.value[a];
          return;
        }
      }
      if (board.value.every((cell) => cell)) {
        winner.value = "Empate";
      }
    };

    const makeMove = (index) => {
      if (!board.value[index] && !winner.value) {
        board.value[index] = currentPlayer.value;
        checkWinner();
        currentPlayer.value = currentPlayer.value === "X" ? "O" : "X";
      }
    };

    const resetGame = () => {
      board.value = Array(9).fill(null);
      currentPlayer.value = "X";
      winner.value = null;
    };

    return {
      board,
      currentPlayer,
      winner,
      winnerMessage,
      makeMove,
      resetGame,
    };
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}
html, body {
  margin: 0;
  padding: 0;
}

#app{
  display: flex;
  flex-direction: column;
  min-height: 71vh;
}
.game {
  font-family: Arial, sans-serif;
  text-align: center;
  margin-top: 50px;
}

.board {
  display: grid;
  grid-template-columns: repeat(3, 100px);
  grid-gap: 5px;
  justify-content: center;
  margin: 20px auto;
}

.cell {
  width: 100px;
  height: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 2px solid #444;
  font-size: 24px;
  font-weight: bold;
  cursor: pointer;
  background-color: #fff;
}

.cell-x {
  color: #2196f3;
}

.cell-o {
  color: #f44336;
}

.winner {
  font-size: 20px;
  color: white;
  margin-top: 20px;
  background: red;
  padding: 10px 10px 10px 10px;
  border-radius: 10px;
}
.reset_Game{
  background-color: green;
  color: white;
  padding: 10px;
}
</style>
