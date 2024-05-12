<template>
<div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm' :''"></div>
<main>
  <div class="search-box">
    <input 
    type="text" 
    placeholder="type to search for location"
    v-model="query"
    @keypress="fetchWeather"
    class="search-bar"/>
  </div>

  <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
    <div class="location-box">
    <div class="location">
      {{ weather.name }}, {{ weather.sys.country }}
    </div>
    <div class="date">
      {{ dateBuilder() }}
    </div>  
  </div>
  </div>
</main>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      weather: {},
      query: "",
      api_key: '9336feb67e548b744acd07195e4dfa3d',
      url_base: 'https://api.openweathermap.org/data/3.0/'
    }
  },
  methods: {
    fetchWeather(e) {
      if(e.key == "Enter") {
        fetch(`${this.url_base}weather?q=${this.query} &units=metric&APPID=${this.api_key}`).then (res => {
          return res.json();
        }).then (this.setResults);
      }
    },
    setResults(results) {
      this.weather = results;
    }
  }
}


</script>

<style>

</style>
