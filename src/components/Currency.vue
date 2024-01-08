<script setup>
import axios from 'axios'
import { ref, onMounted } from 'vue'

const currencyData = ref(null)

onMounted(async () => {
  try {
    const response = await axios.get(
      'https://iss.moex.com/iss/statistics/engines/currency/markets/selt/rates.json?iss.meta=off'
    )
    currencyData.value = response.data
  } catch (error) {
    console.error('Error fetching currency data:', error)
  }
})
</script>

<template>
  <div class="grid grid-cols-4 gap-4 p-4">
    <div
      v-if="currencyData"
      class="relative bg-white border border-slate-100 rounded-2xl p-8 cursor-pointer hover:-translate-y-2 hover:shadow-xl transition-all"
    >
      <p>1 USD = {{ currencyData.wap_rates.data[0][4] }}</p>
    </div>
    <div
      v-if="currencyData"
      class="relative bg-white border border-slate-100 rounded-2xl p-8 cursor-pointer hover:-translate-y-2 hover:shadow-xl transition-all"
    >
      <p>1 EUR = {{ currencyData.wap_rates.data[1][4] }}</p>
    </div>
  </div>
</template>
