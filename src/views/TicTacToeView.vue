<script setup lang="ts">
import { ref } from 'vue'

let count = ref(0)
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
      <div :class="{ active: !hasWinner }" @click="fillSquare(0)" class="square">
        {{ board[0] }}
      </div>
      <div :class="{ active: !hasWinner }" @click="fillSquare(1)" class="square">
        {{ board[1] }}
      </div>
      <div :class="{ active: !hasWinner }" @click="fillSquare(2)" class="square">
        {{ board[2] }}
      </div>
      <div :class="{ active: !hasWinner }" @click="fillSquare(3)" class="square">
        {{ board[3] }}
      </div>
      <div :class="{ active: !hasWinner }" @click="fillSquare(4)" class="square">
        {{ board[4] }}
      </div>
      <div :class="{ active: !hasWinner }" @click="fillSquare(5)" class="square">
        {{ board[5] }}
      </div>
      <div :class="{ active: !hasWinner }" @click="fillSquare(6)" class="square">
        {{ board[6] }}
      </div>
      <div :class="{ active: !hasWinner }" @click="fillSquare(7)" class="square">
        {{ board[7] }}
      </div>
      <div :class="{ active: !hasWinner }" @click="fillSquare(8)" class="square">
        {{ board[8] }}
      </div>
    </div>
    <div>
      <div class="winnerText" v-if="hasWinner">Winner is {{ winningSide }}</div>
    </div>
    <div class="view">
      <button @click="count++">You clicked me {{ count }} times.</button>
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

.square {
  border-radius: 0.5rem;
  margin: 0.5rem;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 2rem;
  transition: all 500ms;
  border: 0.25rem solid black;
}
.square.active {
  border: 0.25rem solid hotpink;
}

.winnerText {
  text-align: center;
}
</style>
