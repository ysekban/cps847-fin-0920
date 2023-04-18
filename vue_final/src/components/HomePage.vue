<script setup>
import { formatISO9075 } from 'date-fns'
defineProps({
  msg: {
    type: String,
    required: true
  }
})
</script>

<script>
import { toRaw } from 'vue'
export default {
  data() {
    return {
      temperature: null,
      myTS: null,
      condition: null
    }
  },
  created() {
    // fetch on init
    this.fetchData()
  },
  methods: {
    async fetchData() {
      const url = `https://api.openweathermap.org/data/2.5/forecast?lat=42.9849&lon=-81.2453&appid=82822e6af70026c1e7a3bf4321043b3e&units=metric`
      this.response = await (await fetch(url)).json()
      this.temperature = toRaw(this.response).list[0].main.temp
      this.condition = toRaw(this.response).list[0].weather[0].description
      this.myTS = toRaw(this.response).list[0].dt
    }
  }
}
</script>


<template>
  <div class="greetings">
    <h1 class="green">{{ msg }}</h1>
	<div id="w-header">Prediction's timestamp: {{ myTS }}</div>
	<div id="w-condition">Condition: {{ condition }}</div>
	<div id="w-temperature">Temperature: {{ temperature }}</div> 
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  top: -10px;
}
h3 {
  font-size: 1.2rem;
}
.greetings h1,
.greetings h3 {
  text-align: center;
}
@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
