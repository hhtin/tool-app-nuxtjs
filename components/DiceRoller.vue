<template>
  <div class="card">
    <h2 class="card-title">Tung Xúc Xắc</h2>
    <div v-for="dice in dices" :key="dice.id" class="dice-row">
      <input
        type="number"
        min="2"
        v-model.number="dice.sides"
        class="input-number"
        @input="updateSides(dice.id, $event.target.value)"
      />
      <span>mặt: {{ dice.result || '-' }}</span>
      <button
        class="button button-red"
        :disabled="dices.length === 1"
        @click="removeDice(dice.id)"
      >
        Xóa
      </button>
    </div>
    <div class="flex-container">
      <button class="button button-green" @click="addDice">
        Thêm Xúc Xắc
      </button>
      <button class="button button-blue" @click="rollDice">
        Tung
      </button>
    </div>
    <div class="history">
      <h3 class="history-title">Lịch sử:</h3>
      <ul class="history-list">
        <li v-for="(result, idx) in history" :key="idx">
          {{ result.join(', ') }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const dices = ref([{ id: 1, sides: 6, result: null }])
const history = ref([])

const addDice = () => {
  dices.value.push({ id: dices.value.length + 1, sides: 6, result: null })
}

const removeDice = (id) => {
  dices.value = dices.value.filter(dice => dice.id !== id)
}

const updateSides = (id, sides) => {
  const parsedSides = parseInt(sides) || 6
  dices.value = dices.value.map(dice =>
    dice.id === id ? { ...dice, sides: parsedSides } : dice
  )
}

const rollDice = () => {
  const results = dices.value.map(dice => ({
    ...dice,
    result: Math.floor(Math.random() * dice.sides) + 1
  }))
  dices.value = results
  history.value.push(results.map(d => d.result))
}
</script>