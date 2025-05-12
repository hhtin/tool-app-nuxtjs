<template>
  <div class="card">
    <h2 class="card-title">Tính Điểm</h2>
    <button class="button button-green full-width" @click="addPlayer">
      Thêm Người Chơi
    </button>
    <div v-for="player in players" :key="player.id" class="player-row">
      <span>{{ player.name }}: {{ player.score }}</span>
      <div class="flex-container">
        <input
          type="number"
          v-model.number="scoreInputs[player.id]"
          placeholder="Điểm"
          class="score-input"
        />
        <button class="button button-blue" @click="applyScoreUpdate(player.id)">
          Cập nhật
        </button>
        <button class="button button-blue" @click="updateScore(player.id, 1)">
          +1
        </button>
        <button class="button button-red" @click="updateScore(player.id, -1)">
          -1
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
const players = ref([])
const scoreInputs = ref({})

onMounted(() => {
  const savedPlayers = localStorage.getItem('players')
  if (savedPlayers) players.value = JSON.parse(savedPlayers)
})

const addPlayer = () => {
  const newPlayer = { id: players.value.length + 1, name: `Người ${players.value.length + 1}`, score: 0 }
  players.value.push(newPlayer)
  localStorage.setItem('players', JSON.stringify(players.value))
}

const updateScore = (id, delta) => {
  players.value = players.value.map(player =>
    player.id === id ? { ...player, score: player.score + delta } : player
  )
  localStorage.setItem('players', JSON.stringify(players.value))
}

const applyScoreUpdate = (id) => {
  const delta = parseInt(scoreInputs.value[id]) || 0
  if (delta !== 0) {
    updateScore(id, delta)
    scoreInputs.value[id] = ''
  }
}
</script>