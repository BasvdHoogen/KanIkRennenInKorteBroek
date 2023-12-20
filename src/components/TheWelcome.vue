<script setup xmlns="http://www.w3.org/1999/html">
import {ref} from 'vue'

const weatherData = ref(null)
// fetch("https://weerlive.nl/api/json-data-10min.php?key=bc398b12be&locatie=Eindhoven").then((r) => r.json()).then(data => weatherData.value = data.liveweer[0])
fetch("https://kortebroekinfo.azurewebsites.net/kortebroekinfo").then((r) => r.json()).then(data => weatherData.value = data)

</script>

<template>
  <div v-if="weatherData != null">
    <div v-if="weatherData.gtemp > 8">
      <h3>JA!</h3>
      Trek je KORTE broek aan. De gevoelstemperatuur is {{ weatherData.gtemp }} °C
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
      <h4>Het weer in {{ weatherData.plaats }}:</h4>
      Temperatuur: {{ weatherData.temp }}<br>
      gevoelstemperatuur: {{ weatherData.gtemp }}<br>
      Samenvatting: {{ weatherData.samenv }}<br>
    </div>
  </div>
  <div v-else>
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