<template>
  <div class="container">
    <h1 class="title">Random Tools</h1>
    <div class="tab-buttons">
      <button
        class="tab-button"
        :class="{ active: activeTab === 'dice' }"
        @click="activeTab = 'dice'"
      >
        Tung Xúc Xắc
      </button>
      <button
        class="tab-button"
        :class="{ active: activeTab === 'wheel' }"
        @click="activeTab = 'wheel'"
      >
        Vòng Quay
      </button>
      <button
        class="tab-button"
        :class="{ active: activeTab === 'score' }"
        @click="activeTab = 'score'"
      >
        Tính Điểm
      </button>
      <button
        class="tab-button"
        :class="{ active: activeTab === 'random' }"
        @click="activeTab = 'random'"
      >
        Bóc Thăm
      </button>
    </div>
    <DiceRoller v-if="activeTab === 'dice'" />
    <Wheel v-if="activeTab === 'wheel'" />
    <ScoreManager v-if="activeTab === 'score'" />
    <RandomDraw v-if="activeTab === 'random'" />
  </div>
</template>

<script setup>
import DiceRoller from '~/components/DiceRoller.vue'
import Wheel from '~/components/Wheel.vue'
import ScoreManager from '~/components/ScoreManager.vue'
import RandomDraw from '~/components/RandomDraw.vue'

const activeTab = ref('dice')
</script>