<template>
  <div class="card">
    <h2 class="card-title">Vòng Quay May Mắn</h2>
    <textarea
      v-model="names"
      placeholder="Nhập tên, mỗi dòng một tên"
      class="textarea"
      rows="5"
      @input="handleNamesChange"
    />
    <button
      class="button full-width"
      :class="spinning ? 'button-gray' : 'button-blue'"
      :disabled="spinning"
      @click="spin"
    >
      {{ spinning ? 'Đang quay...' : 'Quay' }}
    </button>
    <div v-if="result" class="result">
      <h3 class="result-title">Kết quả:</h3>
      <p class="result-text">{{ result }}</p>
    </div>
  </div>
</template>

<script setup>
const names = ref('')
const spinning = ref(false)
const result = ref(null)

onMounted(() => {
  const savedNames = localStorage.getItem('wheelNames')
  if (savedNames) names.value = savedNames
})

const handleNamesChange = () => {
  localStorage.setItem('wheelNames', names.value)
}

const spin = () => {
  const nameList = names.value.split('\n').filter(name => name.trim())
  if (nameList.length === 0) return
  spinning.value = true
  setTimeout(() => {
    const randomIndex = Math.floor(Math.random() * nameList.length)
    result.value = nameList[randomIndex]
    spinning.value = false
  }, 2000)
}
</script>