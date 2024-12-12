<script setup>
import { ref } from 'vue'

const rules = ref({
  length: 8,
  uppercase: false,
  numbers: false,
  symbols: false
})

const generatedPassword = ref('')

const generatePassword = () => {

  let charset = 'abcdefghijklmnopqrstuvwxyz'

  if (rules.value.uppercase) {
    charset += 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
  }

  if (rules.value.numbers) {
    charset += '0123456789'
  }

  if (rules.value.symbols) {
    charset += '!@#$%^&*()'
  }

  let password = ''

  for (let i = 0; i < rules.value.length; i++) {
    const randomIndex = Math.floor(Math.random() * charset.length)
    password += charset.charAt(randomIndex)
  }

  generatedPassword.value = password

  // if (!checkCriterias()) {
  //   return generatePassword()
  // }

}
// const areEquivalent = (x, y) => (x && y) || (!x && !y);

// const checkCriterias = () => {
//   const uppercaseHolder = areEquivalent(rules.value.uppercase, generatePassword.toString().match(/[A-Z]/) !== null)
//   const numbersHolder = areEquivalent(rules.value.numbers, generatePassword.toString().match(/[0-9]/) !== null)
//   const symbolsHolder = areEquivalent(rules.value.symbols, generatePassword.toString().match`/[^a-zA-Z0-9]/` !== null)

//   return uppercaseHolder && numbersHolder && symbolsHolder
// }


</script>


<template>
  <div class="password-generator-container">
    <h2 class="password-generator-title">Password Generator</h2>

    <label for="password-length">Password Length:</label>
    <input type="number" min="8" max="20" name="password-length" id="password-length" v-model="rules.length">

    <label for="uppercase">Include Uppercase</label>
    <input type="checkbox" name="uppercase" id="uppercase" v-model="rules.uppercase">

    <label for="numbers">Include Numbers</label>
    <input type="checkbox" name="numbers" id="numbers" v-model="rules.numbers">

    <label for="symbols">Include Symbols</label>
    <input type="checkbox" name="symbols" id="symbols" v-model="rules.symbols">

    <button type="button" class="generate-button" @click="generatePassword">
      Generate Password
    </button>

    <div class="generated-password">
      Generated Password: {{ generatedPassword }}

    </div>
  </div>
</template>


<style scoped>
.password-generator-container {
  max-width: 400px;
  margin: 50px auto;
}

.password-generator-title {
  font-size: 24px;
  color: #333;
  margin-bottom: 20px;
}

input {
  width: 100%;
  padding: 8px;
  margin-bottom: 10px;
}

.generate-button {
  padding: 10px 15px;
  font-size: 16px;
  background-color: #3498db;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.generate-button:hover {
  background-color: #2980b9;
}

.generated-password {
  margin-top: 20px;
  padding: 15px;
  border: 1px solid #ddd;
  border-radius: 4px;
  background-color: #f9f9f9;
  color: #333;
}
</style>
