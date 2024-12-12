<script setup>
import { ref, computed } from 'vue'

const formData = ref({
  name: '',
  email: '',
  password: '',
  confirmPassword: ''
})

const isNameValid = computed(() => formData.value.name.trim() !== '')
const isEmailValid = computed(() => /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(formData.value.email))
const isPasswordValid = computed(() => formData.value.password.length >= 8)
const isConfirmPasswordValid = computed(() => formData.value.password === formData.value.confirmPassword)

const isFormValid = computed(() => isNameValid.value && isEmailValid.value && isPasswordValid.value && isConfirmPasswordValid.value)

const submitForm = () => {
  if (isFormValid.value) {
    alert('Form submitted successfully!')
    console.log(formData.value)
  }
}
</script>


<template>
  <h1>Form Validation</h1>
  <form class="custom-form" @submit.prevent="submitForm">
    <div class="form-group">
      <label for="">Name</label>
      <input type="text" v-model="formData.name" id="name">
      <p class="error" v-if="!isNameValid">The name is required</p>
    </div>
    <div class="form-group">
      <label for="">Email</label>
      <input type="email" v-model="formData.email" id="email">
      <p class="error" v-if="!isEmailValid">The email is invalid</p>
    </div>
    <div class="form-group">
      <label for="">Password</label>
      <input type="password" v-model="formData.password" id="password">
      <p class="error" v-if="!isPasswordValid">The password must be at least 8 characters long</p>
    </div>
    <div class="form-group">
      <label for="">Confirm Password</label>
      <input type="password" v-model="formData.confirmPassword" id="confirm-password">
      <p class="error" v-if="!isConfirmPasswordValid">The passwords do not match</p>
    </div>
    <button type="submit" class="submit-button" :disabled="!isFormValid">Submit</button>
  </form>
</template>

<style scoped>
.custom-form {
  max-width: 400px;
  margin: 0 auto;
}

.form-group {
  margin-bottom: 20px;
}

label {
  display: block;
  font-weight: bold;
  margin-bottom: 5px;
}

input {
  width: 100%;
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.error {
  color: #e74c3c;
  font-size: 14px;
  margin-top: 5px;
}

.submit-button {
  padding: 10px 15px;
  font-size: 16px;
  background-color: #3498db;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.submit-button:disabled {
  background-color: #bdc3c7;
  cursor: not-allowed;
}
</style>
