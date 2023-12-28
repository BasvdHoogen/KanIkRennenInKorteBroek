<script setup xmlns="http://www.w3.org/1999/html">
import {ref} from 'vue'

const weatherData = ref(null)
fetch("https://kortebroekinfo.azurewebsites.net/kortebroekinfo").then((r) => r.json()).then(data => weatherData.value = data)
// fetch("https://localhost:44301/kortebroekinfo").then((r) => r.json()).then(data => weatherData.value = data)
// fetch("https://api.open-meteo.com/v1/forecast?latitude=51.4408&longitude=5.4778&current=temperature_2m,relative_humidity_2m,apparent_temperature,is_day,precipitation,rain,showers,snowfall,weather_code,cloud_cover,pressure_msl,surface_pressure,wind_speed_10m,wind_direction_10m,wind_gusts_10m&timezone=auto").then((r) => r.json()).then(data => weatherData.value = data)

</script>

<template>
  <div v-if="weatherData != null">
    <div v-if="weatherData.current != null && weatherData.current.apparent_temperature > 8">
      <h3>JA!</h3>
      Trek je KORTE broek aan. De gevoelstemperatuur is {{ weatherData.current.apparent_temperature }} °C
    </div>
    <div v-else-if="weatherData.current != null && weatherData.current.apparent_temperature < 8">
      <h3>Nee!</h3>
      Trek je LANGE broek aan. De gevoelstemperatuur is {{ weatherData.current.apparent_temperature }} °C
    </div>
    <div v-else>
      <h3>Helaas...</h3>
      Er is iets mis gegaan
    </div>
    <br>
    <br>
    <div v-if="weatherData.current != null">
      <h4>Het weer
        <label v-if="weatherData.requestedLocation">in {{ weatherData.requestedLocation }}</label>
        <label v-else>op coördinaat: {{ weatherData.latitude }}, {{ weatherData.longitude }}</label>
      </h4>
      Temperatuur: {{ weatherData.current.temperature_2m }}<br>
      gevoelstemperatuur: {{ weatherData.current.apparent_temperature }}<br>
      coordinaten: {{ weatherData.latitude }}, {{ weatherData.longitude }}
    </div>
  </div>
  <div v-if="weatherData == null">
    <br>
    <br>
    <div class="center">
      <div class="wave"></div>
      <div class="wave"></div>
      <div class="wave"></div>
      <div class="wave"></div>
      <div class="wave"></div>
      <div class="wave"></div>
      <div class="wave"></div>
      <div class="wave"></div>
      <div class="wave"></div>
      <div class="wave"></div>
    </div>
    <div>We laden het weerbericht...</div>
  </div>
</template>

<style scoped>
h3 {
  font-size: 2rem;
  font-weight: 500;
  margin-bottom: 0.4rem;
}

h4 {
  font-size: 1.2rem;
  font-weight: 500;
  margin-bottom: 0.4rem;
}

.center {
  display: flex;
  justify-content: center;
  align-items: center;
}

.wave {
  width: 10px;
  height: 10px;
  background: linear-gradient(1deg, hsla(160, 100%, 37%, 1), hsla(160, 100%, 37%, 1));
  margin: 10px;
  animation: wave 2s linear infinite;
  border-radius: 20px;
}

.wave:nth-child(2) {
  animation-delay: 0.2s;
}

.wave:nth-child(3) {
  animation-delay: 0.4s;
}

.wave:nth-child(4) {
  animation-delay: 0.6s;
}

.wave:nth-child(5) {
  animation-delay: 0.8s;
}

.wave:nth-child(6) {
  animation-delay: 1s;
}

.wave:nth-child(7) {
  animation-delay: 1.2s;
}

.wave:nth-child(8) {
  animation-delay: 1.4s;
}

.wave:nth-child(9) {
  animation-delay: 1.6s;
}

.wave:nth-child(10) {
  animation-delay: 1.8s;
}

@keyframes wave {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(0);
  }
  100% {
    transform: scale(0);
  }
}
</style>