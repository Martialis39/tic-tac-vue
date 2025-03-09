<script setup lang="ts">
import { ref } from 'vue'
import Square from '../components/Square.vue'

let turn = ref('X')
let hasWinner = ref(false)
let winningSide = ref('')
let board = ref(['', '', '', '', '', '', '', '', ''])
function fillSquare(i: number) {
  if (hasWinner.value) {
    return
  }
  board.value = board.value.map((s, index) => {
    if (i == index && s === '') {
      return turn.value
    }
    return s
  })

  // Check win

  if (checkWin(board.value, turn.value)) {
    hasWinner.value = true
    winningSide.value = turn.value
    return
  }

  // Switch turn

  if (turn.value === 'X') {
    turn.value = 'O'
  } else {
    turn.value = 'X'
  }
}

function checkWin(board: string[], playerSymbol: string): boolean {
  let winningCombinations = [
    // rows
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    // columns
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    // diagonals
    [0, 4, 8],
    [2, 4, 6],
  ]

  const boardInWinningState = winningCombinations.some((combination: number[]) => {
    let [a, b, c] = combination
    if (board[a] === playerSymbol && board[b] === playerSymbol && board[c] === playerSymbol) {
      return true
    } else {
      return false
    }
  })

  return boardInWinningState
}
</script>

<template>
  <div class="wrapper">
    <div class="board">
      <Square
        v-for="(item, index) in board"
        :content="item"
        :active="!hasWinner"
        @fill="
          () => {
            fillSquare(index)
          }
        "
      />
    </div>
    <div>
      <div class="winnerText" v-if="hasWinner">Winner is {{ winningSide }}</div>
    </div>
  </div>
</template>

<style>
.board {
  max-width: 450px;
  height: 450px;
  width: 100%;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: 1fr 1fr 1fr;
}

.winnerText {
  text-align: center;
}
</style>
