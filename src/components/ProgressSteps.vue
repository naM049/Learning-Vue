<script setup>
import { shallowRef } from 'vue'
import RandomQuoteGenerator from './RandomQuoteGenerator.vue';
import FormValidation from './FormValidation.vue';
import PasswordGenerator from './PasswordGenerator.vue';
import AmazingCalculator from './AmazingCalculator.vue';

const tabs = shallowRef([
  RandomQuoteGenerator,
  FormValidation,
  PasswordGenerator,
  AmazingCalculator
])
const currentTab = shallowRef(RandomQuoteGenerator)

const nextTab = () => {
  const currentIndex = tabs.value.indexOf(currentTab.value)
  if (currentIndex < tabs.value.length - 1) {
    currentTab.value = tabs.value[currentIndex + 1]
  }
}

const previousTab = () => {
  const currentIndex = tabs.value.indexOf(currentTab.value)
  if (currentIndex > 0) {
    currentTab.value = tabs.value[currentIndex - 1]
  }
}
</script>

<template>
  <h1>Progress Steps</h1>

  <div class="progress-container">
    <div class="progress-bar">
      <div v-for="(tab, index) of tabs" :key="index" :class="{ 'step-active': currentTab === tab }" @click="currentTab = tab"> Tab {{ index + 1 }}</div>
    </div>

    <KeepAlive>
      <component :is="currentTab"></component>
    </KeepAlive>

    <div class="controls">
      <button class="btn" @click="previousTab" :disabled="tabs.indexOf(currentTab) === 0">Previous</button>
      <button class="btn" @click="nextTab" :disabled="tabs.indexOf(currentTab) === tabs.length - 1">Next</button>
    </div>
  </div>
</template>


<style scoped>
.progress-container {
  max-width: 400px;
  margin: 50px auto;
}

.progress-bar {
  display: flex;
  background-color: #eee;
  border-radius: 8px;
  overflow: hidden;
}

.progress-bar div {
  flex: 1;
  text-align: center;
  padding: 15px;
  color: #fff;
  position: relative;
  z-index: 1;
  cursor: pointer;
}

.progress-bar div:not(:last-child) {
  border-right: 2px solid #fff;
}

.step-active {
  background-color: #af514c;
}

.controls {
  margin-top: 20px;
  text-align: center;
}

.btn {
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
  background-color: #673ab7;
  color: #fff;
  border: none;
  border-radius: 5px;
  margin: 0 5px;
}

.btn:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}
</style>
