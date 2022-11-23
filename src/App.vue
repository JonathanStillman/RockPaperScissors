<script setup>
import {ref, computed, onMounted } from 'vue';

// Setting variables
const wins = ref(0)
const draws = ref(0)
const losses = ref(0)

const choice = ref(null)
const computerChoice = ref(null)
const verdict = ref(null)

// Outcomes
const outcomes = {
  rock: {
    rock: 'draw',
    paper: 'loss',
    scissors: 'win',
  },
  paper: {
    rock: 'win',
    paper: 'draw',
    scissors: 'loss',
  },
  scissors: {
    rock: 'loss',
    paper: 'win',
    scissors: 'draw',
  }
}

// Win percentage
const winPercentage = computed(() => {
  const total = wins.value + draws.value + losses.value
  return total ? (wins.value / total) * 100 : 0
})


const play = c => {
  choice.value = c

  const choices = ['rock', 'paper', 'scissors']
  const random = Math.floor(Math.random() * choices.length)
  computerChoice.value = choices[random]

  const outcome = outcomes[c][computerChoice.value]

  if (outcome === 'win') {
    wins.value++
    verdict.value = 'You win!'
  } else if (outcome === 'loss') {
    losses.value++
    verdict.value = 'You lose!'
  } else {
    draws.value++
    verdict.value = 'It is a draw!'
  }

  SaveGame()
}

// Saving Game
const SaveGame = () => {
  localStorage.setItem('wins', wins.value)
  localStorage.setItem('draws', draws.value)
  localStorage.setItem('losses', losses.value)
}

// Loading Game
const LoadGame = () => {
  wins.value = localStorage.getItem('wins')
  draws.value = localStorage.getItem('draws')
  losses.value = localStorage.getItem('losses')
}

// Resetting round
const ResetRound = () => {
  choice.value = null
  computerChoice.value = null
  verdict.value = null
}


onMounted(() => {
  LoadGame()

  window.addEventListener('keypress', e => {
    if (e.key === 'r') {
      ResetRound()
    }
  })
})

</script>

<template>
  <div class="bg-gray-700 text-white text-center min-h-screen flex flex-col">

  </div>
</template>

<style scoped>

</style>
