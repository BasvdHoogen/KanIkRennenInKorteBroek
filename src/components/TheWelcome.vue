<script setup xmlns="http://www.w3.org/1999/html">
import {ref} from 'vue'

const weather = ref(null)
const weatherData = ref(null)
fetch("https://weerlive.nl/api/json-data-10min.php?key=bc398b12be&locatie=Eindhoven").then((r) => r.json()).then(data => weatherData.value = data.liveweer[0])

</script>

<template>
  <div v-if="weatherData != null">
    <div v-if="weatherData.gtemp > 8">
      <h3>JA!</h3>
      Trek je KORTE broek aan. De gevoelstemperatuur is {{ weatherData.gtemp }} °C
      <br>
      <div><img src="/man-running-emoji-258749.png" alt="man-running-emoji-with-short-pants"
                style="width:128px;height:128px;"></div>
    </div>
    <div v-else-if="weatherData.gtemp < 8">
      <h3>Nee!</h3>
      Trek je LANGE broek aan. De gevoelstemperatuur is {{ weatherData.gtemp }} °C
    </div>
    <div v-else>
      <h3>Helaas...</h3>
      Er is iets mis gegaan
    </div>
    <br>
    <br>
    <div>
      <h3>Weer van {{weatherData.plaats}}:</h3>
      Temperatuur: {{ weatherData.temp }}<br>
      gevoelstemperatuur: {{ weatherData.gtemp }}<br>
      Samenvatting: {{ weatherData.samenv }}<br>

    </div>
  </div>

</template>

<style scoped>
h3 {
  font-size: 1.2rem;
  font-weight: 500;
  margin-bottom: 0.4rem;
}
</style>