<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'

const dadJoke = ref('')

const getJoke = async () => {
  await axios.get('https://icanhazdadjoke.com/', {
    headers: {
      'Accept': 'application/json'
    }
  }).then(response => {
    dadJoke.value = response.data.joke
  }).catch(error => {
    console.error(error)
  })
}

onMounted(getJoke)
</script>

<template>
  <div class="dad-jokes-container">
    <h2 class="dad-jokes-title">Dad Jokes</h2>
    <div class="dad-joke">{{ dadJoke }}</div>
    <button type="button" class="get-joke-button" @click="getJoke">Get a Joke</button>
  </div>
</template>

<style scoped>
.dad-jokes-container {
  max-width: 600px;
  margin: 50px auto;
}

.dad-jokes-title {
  font-size: 24px;
  color: #333;
  margin-bottom: 20px;
}

.get-joke-button {
  padding: 10px 15px;
  font-size: 16px;
  background-color: #4caf50;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  margin-top: 20px;
}

.get-joke-button:hover {
  background-color: #45a049;
}

.dad-joke {
  border: 1px solid #ddd;
  border-radius: 4px;
  padding: 15px;
  margin-top: 20px;
  background-color: #f9f9f9;
  color: #333;
}
</style>
