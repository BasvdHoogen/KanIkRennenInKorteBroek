<script setup>
import WelcomeItem from './WelcomeItem.vue'
import EcosystemIcon from './icons/IconEcosystem.vue'
import {ref} from 'vue'

const weather = ref(null)
const weatherData = ref(null)
fetch("https://weerlive.nl/api/json-data-10min.php?key=demo&locatie=Amsterdam").then((r) => r.json()).then(data => weatherData.value = data.liveweer[0].temp)

</script>

<template>
  <div v-if="weatherData > 8">
    <h3>JA!</h3>
    Trek je korte broek aan. Het is {{ weatherData }} graden!
  </div>
  <div v-else-if="weatherData < 8">
    <h3>Nee!</h3>
    Trek je LANGE broek aan. Het is {{ weatherData }} graden!
  </div>
  <div v-else>
    <h3>Helaas...</h3>
    Er is iets mis gegaan
  </div>
</template>

<style scoped>
h3 {
  font-size: 1.2rem;
  font-weight: 500;
  margin-bottom: 0.4rem;
  color: var(--color-heading);
}
</style>