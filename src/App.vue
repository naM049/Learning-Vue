<script setup>
import { ref, computed } from 'vue'

import TodoList from "./components/TodoList.vue"
import RandomQuoteGenerator from "./components/RandomQuoteGenerator.vue"
import AmazingCalculator from './components/AmazingCalculator.vue';
import AccordionComponent from './components/AccordionComponent.vue';
import FormValidation from './components/FormValidation.vue';
import PasswordGenerator from './components/PasswordGenerator.vue';
import ProgressSteps from './components/ProgressSteps.vue';
import DadJokes from './components/DadJokes.vue';
import GithubUsersSearch from './components/GithubUsersSearch.vue';

const routes = {
  '/todolist': TodoList,
  '/randomquote': RandomQuoteGenerator,
  '/amazingcalculator': AmazingCalculator,
  '/accordioncomponent': AccordionComponent,
  '/formvalidation': FormValidation,
  '/passwordgenerator': PasswordGenerator,
  '/progresssteps': ProgressSteps,
  '/dadjokes': DadJokes,
  '/githubuserssearch': GithubUsersSearch
}

const currentPath = ref(window.location.hash)

window.addEventListener('hashchange', () => {
  currentPath.value = window.location.hash
})

const currentView = computed(() => {
  return routes[currentPath.value.slice(1) || '/']
})
</script>

<template>
  <div class="links">
  <a href="#/todolist">Todo List</a>
  <a href="#/randomquote">Random Quote Generator</a>
  <a href="#/amazingcalculator">Amazing Calculator</a>
  <a href="#/accordioncomponent">Accordion</a>
  <a href="#/formvalidation">Form Validation</a>
  <a href="#/passwordgenerator">Password Generator</a>
  <a href="#/progresssteps">Progress Steps</a>
  <a href="#/dadjokes">Dad Jokes</a>
  <a href="#/githubuserssearch">Github User Search</a>
  </div>

  <KeepAlive>
    <component :is="currentView" />
  </KeepAlive>
</template>

<style scoped>
.links {
  display: flex;
  gap: 10px;
  margin-bottom: 10px;

}
a {
  color: #692bdd;
  text-decoration: none;
}
</style>
