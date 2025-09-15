<template>
  <div class="card">
    <h2 class="card-title">Bóc Thăm Ngẫu Nhiên</h2>
    <textarea
      v-model="randomList"
      placeholder="Nhập danh sách, mỗi dòng một mục"
      class="textarea"
      rows="5"
      @input="handleRandomListChange"
    />
    <div class="flex-container">
      <button class="button button-blue" @click="drawRandom">
        Bóc Thăm
      </button>
      <button class="button button-gray" @click="resetRandom">
        Reset
      </button>
    </div>
    <div v-if="randomResult" class="result">
      <h3 class="result-title">Kết quả:</h3>
      <p class="result-text">{{ randomResult }}</p>
    </div>
  </div>
</template>

<script setup>
const randomList = ref('')
const randomResult = ref(null)
const originalList = ref('')

onMounted(() => {
  const savedRandomList = localStorage.getItem('randomList')
  if (savedRandomList) {
    randomList.value = savedRandomList
    originalList.value = savedRandomList
  }
})

const drawRandom = () => {
  const items = randomList.value.split('\n').filter(item => item.trim())
  if (items.length === 0) return
  const randomIndex = Math.floor(Math.random() * items.length)
  const selected = items[randomIndex]
  randomResult.value = selected
  const newList = items.filter((_, idx) => idx !== randomIndex).join('\n')
  randomList.value = newList
  localStorage.setItem('randomList', newList)
}

const resetRandom = () => {
  randomList.value = originalList.value
  randomResult.value = null
  localStorage.setItem('randomList', originalList.value)
}

const handleRandomListChange = () => {
  originalList.value = randomList.value
  localStorage.setItem('randomList', randomList.value)
}
</script>