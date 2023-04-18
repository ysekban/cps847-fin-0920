<script setup>
import HomePage from '../components/HomePage.vue'
</script>

<template>
  <main>
    <HomePage />
  </main>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
