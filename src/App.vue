<script setup>
import Currency from './components/Currency.vue'
import kommersantNewsVue from './components/kommersantNews.vue'
import Weather from './components/Weather.vue'
</script>

<template>
  <Currency />
  <Weather cityName="kaliningrad" />
  <kommersantNewsVue />
</template>

<style scoped></style>
