<script setup lang="ts">
import { ref } from 'vue'

let count = ref(0)
let turn = ref('X')
let board = ref(['', '', '', '', '', '', '', '', ''])
function fillSquare(i: number) {
  board.value = board.value.map((s, index) => {
    if (i == index && s === '') {
      return turn.value
    }
    return s
  })

  if (turn.value === 'X') {
    turn.value = 'O'
  } else {
    turn.value = 'X'
  }
}
</script>

<template>
  <div class="wrapper">
    <div class="board">
      <div @click="fillSquare(0)" class="square">{{ board[0] }}</div>
      <div @click="fillSquare(1)" class="square">{{ board[1] }}</div>
      <div @click="fillSquare(2)" class="square">{{ board[2] }}</div>
      <div @click="fillSquare(3)" class="square">{{ board[3] }}</div>
      <div @click="fillSquare(4)" class="square">{{ board[4] }}</div>
      <div @click="fillSquare(5)" class="square">{{ board[5] }}</div>
      <div @click="fillSquare(6)" class="square">{{ board[6] }}</div>
      <div @click="fillSquare(7)" class="square">{{ board[7] }}</div>
      <div @click="fillSquare(8)" class="square">{{ board[8] }}</div>
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
  border: 0.25rem solid hotpink;
  border-radius: 0.5rem;
  margin: 0.5rem;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 2rem;
}
</style>
