<script setup>
import axios from 'axios'
import { ref, onMounted } from 'vue'

// Define props directly without using props object
const { cityName } = defineProps(['cityName'])

// Define a reactive ref to store the API response
const weatherData = ref(null)

const kelvinToCelsius = (kelvin) => kelvin - 273.15

// Fetch data from the API when the component is mounted
onMounted(async () => {
  try {
    const response = await axios.get(
      `https://api.openweathermap.org/data/2.5/weather?q=${cityName}&appid=`
    )
    weatherData.value = response.data
  } catch (error) {
    console.error('Error fetching weather data:', error)
  }
})
</script>

<template>
  <div class="grid gap-5 p-4">
    <div
      class="relative bg-white border border-slate-100 rounded-2xl p-8 cursor-pointer hover:-translate-y-2 hover:shadow-xl transition-all"
    >
      <p>Weather in {{ cityName }}:</p>
      <p v-if="weatherData" class="text-2xl">
        {{ kelvinToCelsius(weatherData.main.temp).toFixed(0) }} ºC
      </p>
      <p v-if="weatherData" class="text-1xl">humidity: {{ weatherData.main.humidity }}</p>
      <p v-if="weatherData" class="text-1xl">{{ weatherData.weather[0].main }}</p>
    </div>
  </div>
</template>
