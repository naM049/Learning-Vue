<script setup>
import { ref } from 'vue'
import axios from 'axios';


const username = ref('')
const user = ref(null)
const errorMessage = ref('')

const getUser = async () => {
  errorMessage.value = ''
  user.value = null

  if (username.value.trim() === '') {
    alert('Please enter a GitHub username')
    return
  }

  await axios.get(`https://api.github.com/users/${username.value}`)
  .then(response => {
    user.value = response.data
  })
  .catch(error => {
    console.error(error)
    errorMessage.value = 'User not found'
  })
}
</script>


<template>
  <div class="github-profile-viewer">
    <h2 class="apptitle">Github Profile Viewer</h2>
    <div class="inpout-container">
      <input type="text" name="username" id="username" v-model="username" @keydown.enter="getUser" placeholder="Enter a GitHub username">
    </div>

    <div class="user-details" v-if="user">
      <img :src="user.avatar_url" alt="" class="user-profile">
      <p>Name: {{ user.name }} </p>
      <p>Public repos: {{ user.public_repos }} </p>
      <p>Followers: {{ user.followers }}</p>
      <p>Following: {{ user.following }}</p>
      <p>Location: {{ user.location }}</p>

    </div>

    <p v-if="errorMessage" class="error-message">{{ errorMessage }}</p>
  </div>
</template>


<style scoped>
.github-profile-viewer {
  max-width: 600px;
  margin: 50px auto;
  padding: 20px;
  text-align: center;
  border: 1px solid #ccc;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.app-title {
  font-size: 24px;
  margin-bottom: 20px;
  color: #333;
}

.input-container {
  margin-bottom: 20px;
}

input {
  width: 100%;
  padding: 10px 0;
  font-size: 16px;
}

.user-profile {
  margin-top: 20px;
}

h2 {
  font-size: 20px;
  margin-bottom: 10px;
  color: #333;
}

img {
  width: 150px;
  border-radius: 50%;
  margin-bottom: 20px;
}

.user-details {
  text-align: left;
}

p {
  font-size: 16px;
  margin-bottom: 10px;
}

.error-message {
  color: #e74c3c;
  margin-top: 20px;
}
</style>
