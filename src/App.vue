<template>
  <div id="app">
    <div class="hero-background">
      <video
        autoplay
        loop
        muted
        playsinline
        class="hero-video"
      >
        <source src="/animations/Number_System_Conversion_Animation.mp4" type="video/mp4" />
      </video>
      <div class="overlay"></div>
    </div>
    <div class="hero-content">
      <h1 class="animated-title">Number System Conversion</h1>
      <div class="conversion-boxes">
        <div 
          v-for="base in bases" 
          :key="base.name"
          class="conversion-box"
          @click="openModal(base.name)"
        >
          <h2>{{ base.label }}</h2>
          <p>{{ base.name }}</p>
        </div>
      </div>
    </div>

    <!-- Modal -->
    <div v-if="showModal" class="modal-overlay" @click.self="closeModal">
      <div class="modal-content">
        <div class="modal-header">
          <h2>Convert from {{ currentBase }}</h2>
          <button class="close-button" @click="closeModal">&times;</button>
        </div>
        <div class="modal-body">
          <div class="input-group">
            <label>Input Value ({{ currentBase }})</label>
            <input 
              v-model="inputValue" 
              type="text" 
              :placeholder="`Enter ${currentBase} value`"
              class="input-field"
            />
          </div>
          <div class="input-group">
            <label>Convert to</label>
            <select v-model="targetBase" class="select-field">
              <option v-for="base in availableBases" :key="base" :value="base">
                {{ base }}
              </option>
            </select>
          </div>
          <button class="convert-button" @click="convert">Convert</button>
          <div v-if="result" class="result">
            <label>Result:</label>
            <div class="result-value">{{ result }}</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'

const bases = [
  { name: 'decimal', label: 'Decimal' },
  { name: 'binary', label: 'Binary' },
  { name: 'hexadecimal', label: 'Hexadecimal' },
  { name: 'octal', label: 'Octal' }
]

const showModal = ref(false)
const currentBase = ref('')
const inputValue = ref('')
const targetBase = ref('')
const result = ref('')

const availableBases = computed(() => {
  return bases.filter(b => b.name !== currentBase.value).map(b => b.name)
})

const openModal = (base: string) => {
  currentBase.value = base
  targetBase.value = availableBases.value[0]
  inputValue.value = ''
  result.value = ''
  showModal.value = true
}

const closeModal = () => {
  showModal.value = false
  inputValue.value = ''
  result.value = ''
}

const convert = () => {
  if (!inputValue.value.trim()) {
    alert('Please enter a value')
    return
  }

  try {
    let decimalValue: number

    // Convert input to decimal first
    switch (currentBase.value) {
      case 'decimal':
        decimalValue = parseInt(inputValue.value, 10)
        break
      case 'binary':
        decimalValue = parseInt(inputValue.value, 2)
        break
      case 'hexadecimal':
        decimalValue = parseInt(inputValue.value, 16)
        break
      case 'octal':
        decimalValue = parseInt(inputValue.value, 8)
        break
      default:
        throw new Error('Invalid base')
    }

    if (isNaN(decimalValue)) {
      throw new Error('Invalid input value')
    }

    // Convert from decimal to target base
    switch (targetBase.value) {
      case 'decimal':
        result.value = decimalValue.toString(10)
        break
      case 'binary':
        result.value = decimalValue.toString(2)
        break
      case 'hexadecimal':
        result.value = decimalValue.toString(16).toUpperCase()
        break
      case 'octal':
        result.value = decimalValue.toString(8)
        break
      default:
        throw new Error('Invalid target base')
    }
  } catch (error) {
    alert('Invalid input. Please check your value.')
    result.value = ''
  }
}
</script>

<style scoped>
#app {
  position: relative;
  width: 100%;
  height: 100vh;
  overflow: hidden;
}

.hero-background {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 0;
  filter: blur(4px);
  overflow: hidden;
}

.hero-video {
  width: 100%;
  height: 100%;
  object-fit: cover;
  opacity: 0.6;
}

.overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  backdrop-filter: blur(2px);
}

.hero-content {
  position: relative;
  z-index: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  text-align: center;
  padding: 2rem;
  box-sizing: border-box;
}

.animated-title {
  font-size: 4em;
  color: #42b983;
  text-shadow: 2px 2px 8px rgba(0, 0, 0, 0.8);
  animation: fadeInUp 1.2s ease-out;
  margin-bottom: 2rem;
}

.conversion-boxes {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1.5rem;
  max-width: 900px;
  width: 100%;
  margin-top: 1rem;
}

.conversion-box {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  border: 2px solid rgba(66, 185, 131, 0.3);
  border-radius: 15px;
  padding: 2rem;
  cursor: pointer;
  transition: all 0.3s ease;
  animation: fadeInUp 1.5s ease-out;
}

.conversion-box:hover {
  transform: translateY(-5px);
  border-color: #42b983;
  background: rgba(66, 185, 131, 0.2);
  box-shadow: 0 8px 25px rgba(66, 185, 131, 0.4);
}

.conversion-box h2 {
  color: #42b983;
  margin: 0 0 0.5rem 0;
  font-size: 1.8em;
  text-shadow: 1px 1px 3px rgba(0, 0, 0, 0.5);
}

.conversion-box p {
  color: rgba(255, 255, 255, 0.8);
  margin: 0;
  text-transform: capitalize;
  font-size: 0.9em;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Modal Styles */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.7);
  backdrop-filter: blur(5px);
  z-index: 1000;
  display: flex;
  align-items: center;
  justify-content: center;
  animation: fadeIn 0.3s ease-out;
}

.modal-content {
  background: rgba(30, 30, 30, 0.95);
  backdrop-filter: blur(20px);
  border: 2px solid rgba(66, 185, 131, 0.5);
  border-radius: 20px;
  padding: 2rem;
  max-width: 500px;
  width: 90%;
  max-height: 90vh;
  overflow-y: auto;
  animation: slideUp 0.3s ease-out;
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1.5rem;
}

.modal-header h2 {
  color: #42b983;
  margin: 0;
  text-transform: capitalize;
}

.close-button {
  background: transparent;
  border: none;
  color: white;
  font-size: 2em;
  cursor: pointer;
  line-height: 1;
  padding: 0;
  width: 30px;
  height: 30px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  transition: all 0.2s ease;
}

.close-button:hover {
  background: rgba(255, 255, 255, 0.1);
  transform: rotate(90deg);
}

.modal-body {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.input-group {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.input-group label {
  color: rgba(255, 255, 255, 0.9);
  font-weight: 500;
  text-transform: capitalize;
}

.input-field,
.select-field {
  padding: 0.75rem;
  border: 2px solid rgba(66, 185, 131, 0.3);
  border-radius: 8px;
  background: rgba(255, 255, 255, 0.1);
  color: white;
  font-size: 1em;
  transition: all 0.3s ease;
}

.input-field:focus,
.select-field:focus {
  outline: none;
  border-color: #42b983;
  background: rgba(255, 255, 255, 0.15);
}

.select-field {
  cursor: pointer;
  background: #000000;
}

.select-field:focus {
  background: #000000;
}

.select-field option {
  background: #000000;
  color: white;
  padding: 0.5rem;
}

.convert-button {
  padding: 1rem 2rem;
  font-size: 1.1em;
  font-weight: 600;
  color: white;
  background: linear-gradient(135deg, #42b983 0%, #35a372 100%);
  border: none;
  border-radius: 10px;
  cursor: pointer;
  box-shadow: 0 4px 15px rgba(66, 185, 131, 0.4);
  transition: all 0.3s ease;
  margin-top: 0.5rem;
}

.convert-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(66, 185, 131, 0.6);
  background: linear-gradient(135deg, #4dd4a3 0%, #42b983 100%);
}

.convert-button:active {
  transform: translateY(0);
}

.result {
  margin-top: 1rem;
  padding: 1rem;
  background: rgba(66, 185, 131, 0.1);
  border: 2px solid rgba(66, 185, 131, 0.3);
  border-radius: 10px;
}

.result label {
  color: rgba(255, 255, 255, 0.8);
  display: block;
  margin-bottom: 0.5rem;
  font-weight: 500;
}

.result-value {
  color: #42b983;
  font-size: 1.5em;
  font-weight: 600;
  word-break: break-all;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@keyframes slideUp {
  from {
    transform: translateY(50px);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}

@media (max-width: 768px) {
  .conversion-boxes {
    grid-template-columns: repeat(2, 1fr);
    gap: 1rem;
  }
  
  .animated-title {
    font-size: 2.5em;
  }
  
  .conversion-box {
    padding: 1.5rem;
  }
  
  .conversion-box h2 {
    font-size: 1.4em;
  }
}
</style>
