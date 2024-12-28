<script setup lang="ts">
import { ref, onMounted } from 'vue'
import PatternDividerDesktop from './icons/PatternDividerDesktop.vue'
import DiceIcon from './icons/DiceIcon.vue'

const advice = ref<string>('')
const id = ref<string>('')

const fetchAdvice = async () => {
  return await fetch('https://api.adviceslip.com/advice')
    .then((res) => res.json())
    .then(({ slip }) => {
      advice.value = slip.advice
      id.value = slip.id
    })
    .error((err) => console.log('Error detected!', err))
}

onMounted(() => {
  fetchAdvice()
})
</script>

<template>
  <div class="advice__container">
    <span class="advice__number">ADVICE #{{ id }}</span>
    <p class="advice__description">
      {{ advice }}
    </p>
    <PatternDividerDesktop></PatternDividerDesktop>
    <button class="advice__dice-container" @click="fetchAdvice">
      <DiceIcon></DiceIcon>
    </button>
  </div>
</template>

<style scoped>
.advice__container {
  align-items: center;
  display: flex;
  flex-direction: column;
  padding: 16px 24px 0;
  max-width: 700px;
}

.advice__number {
  color: #59fcad;
  font-weight: 700;
  letter-spacing: 5px;
}

.advice__description {
  color: #cee3e9;
  font-size: 34px;
  font-weight: 700;
  text-align: center;
}

.advice__dice-container {
  aspect-ratio: 1;
  background-color: #59fcad;
  border: none;
  clip-path: circle();
  margin-bottom: -26px;
  padding: 16px;
  transition: scale ease-in-out 0.1s;
}

.advice__dice-container:hover {
  cursor: pointer;
}

.advice__dice-container:active {
  scale: 0.95;
}
</style>
