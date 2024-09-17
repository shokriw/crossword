<template>
  <div class="min-h-screen bg-gray-100 flex items-center justify-center p-6">
    <div class="bg-white rounded-lg shadow-xl p-8 max-w-2xl w-full">
      <h1 class="text-3xl font-bold text-center mb-6">5x5 Crossword Puzzle</h1>
      
      <div class="grid grid-cols-5 gap-1 mb-8">
        <template v-for="(row, rowIndex) in puzzle" :key="rowIndex">
          <div 
            v-for="(cell, colIndex) in row" 
            :key="`${rowIndex}-${colIndex}`"
            class="relative"
          >
            <input 
              v-model="puzzle[rowIndex][colIndex]"
              type="text"
              maxlength="1"
              class="w-12 h-12 text-center text-xl font-bold uppercase border border-gray-300 focus:border-blue-500 focus:ring focus:ring-blue-200 focus:ring-opacity-50"
              @input="checkSolution"
            >
            <span 
              v-if="cellNumbers[`${rowIndex}-${colIndex}`]"
              class="absolute top-0 left-0 text-xs font-semibold text-gray-500 p-1"
            >
              {{ cellNumbers[`${rowIndex}-${colIndex}`] }}
            </span>
          </div>
        </template>
      </div>

      <div class="grid grid-cols-2 gap-8">
        <div>
          <h2 class="text-xl font-semibold mb-2">Across</h2>
          <ol class="list-decimal list-inside">
            <li v-for="clue in acrossClues" :key="clue">{{ clue }}</li>
          </ol>
        </div>
        <div>
          <h2 class="text-xl font-semibold mb-2">Down</h2>
          <ol class="list-decimal list-inside">
            <li v-for="clue in downClues" :key="clue">{{ clue }}</li>
          </ol>
        </div>
      </div>

      <div v-if="isSolved" class="mt-6 text-center text-green-600 font-bold text-xl">
        Congratulations! You solved the puzzle!
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive, computed } from 'vue'

const puzzle = reactive([
  ['', '', '', '', ''],
  ['', '', '', '', ''],
  ['', '', '', '', ''],
  ['', '', '', '', ''],
  ['', '', '', '', ''],
])

const solution = [
  ['S', 'P', 'A', 'C', 'E'],
  ['T', 'R', 'A', 'I', 'N'],
  ['A', 'I', 'S', 'L', 'E'],
  ['R', 'D', 'K', 'E', 'W'],
  ['T', 'E', 'Y', 'E', 'S'],
]

const cellNumbers = {
  '0-0': 1,
  '0-3': 2,
  '1-0': 3,
  '2-0': 4,
  '2-2': 5,
  '3-3': 6,
  '4-2': 7,
  '4-4': 8,
}

const acrossClues = [
  '1. The final frontier',
  '3. Locomotive',
  '4. Walkway between seats',
  '7. Organs of sight',
  '8. Affirmative responses',
]

const downClues = [
  '1. Begin a journey',
  '2. Feline',
  '3. Celestial body',
  '5. Curved path of a celestial object',
  '6. New (prefix)',
]

const isSolved = ref(false)

const checkSolution = () => {
  isSolved.value = puzzle.every((row, rowIndex) => 
    row.every((cell, colIndex) => 
      cell.toLowerCase() === solution[rowIndex][colIndex].toLowerCase()
    )
  )
}
</script>
