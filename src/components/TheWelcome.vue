<script setup xmlns="http://www.w3.org/1999/html" lang="ts">
import {ref, Ref} from 'vue'
import LoadingWave from "@/components/Loading-wave.vue";
import {} from "vue";

const weatherData = ref(null)
const successful: Ref<boolean | null> = ref<boolean>(null)
const loading: Ref<boolean> = ref<boolean>(true)
fetch("https://kortebroekinfo.azurewebsites.net/kortebroekinfo")
// fetch("http://localhost:5195/kortebroekinfo?location=Eindhoven")
    .then((r) => r.json())
    .then((data) => {
      loading.value = false;
      weatherData.value = data.weatherForecast;
      successful.value = data.succesfull;
    })
</script>

<template>
  <loading-wave v-if="loading" />
  <div v-else>
    <div v-if="successful == true && weatherData != null">
        <div v-if="weatherData.current != null && weatherData.current.apparent_temperature > 8">
          <h3>JA!</h3>
          Trek je KORTE broek aan. De gevoelstemperatuur is {{ weatherData.current.apparent_temperature }} °C
        </div>
        <div v-else-if="weatherData.current != null && weatherData.current.apparent_temperature < 8">
          <h3>Nee!</h3>
          Trek je LANGE broek aan. De gevoelstemperatuur is {{ weatherData.current.apparent_temperature }} °C
        </div>

        <br>
        <br>
        <div v-if="weatherData.current != null">
          <h4>Het weer
            <span v-if="weatherData.requestedLocation">in {{ weatherData.requestedLocation }}</span>
            <span v-else>op coördinaat: {{ weatherData.latitude }}, {{ weatherData.longitude }}</span>
          </h4>
          Coördinaten: {{ weatherData.latitude }}, {{ weatherData.longitude }}<br><br>
          Temperatuur: {{ weatherData.current.temperature_2m }} {{weatherData.current_units.temperature_2m}}<br>
          Gevoelstemperatuur: {{ weatherData.current.apparent_temperature }} {{weatherData.current_units.apparent_temperature}}<br>
          Wind: {{weatherData.current.wind_speed_10m}} {{weatherData.current_units.wind_speed_10m}}<br>
          Beschrijving: {{weatherData.current.weather_code_string}}
        </div>
    </div>
    <div v-else>
      <h3>Helaas...</h3>
      Er is iets mis gegaan
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
</style>