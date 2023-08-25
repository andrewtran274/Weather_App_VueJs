<template>
  <div>
    <h1 v-if="weatherData">Weather in {{ weatherData.name }}</h1>
    <p v-if="weatherData">Temperature: {{ weatherData.main.temp }}°C</p>
    <p v-if="weatherData">Humidity: {{ weatherData.main.humidity }}%</p>
    <img v-if="weatherData" :src="weatherIconUrl" alt="Weather Icon" />
    <p v-else>Enter a city name to get the weather.</p>
  </div>
</template>

<script>
import axios from "axios";

export default {
  props: {
    apiKey: String,
    city: String,
  },
  data() {
    return {
      defaultCity: "DefaultCityName",
      weatherData: null,
    };
  },
  computed: {
    weatherIconUrl() {
      if (
        this.weatherData &&
        this.weatherData.weather &&
        this.weatherData.weather.length > 0
      ) {
        // Assuming that the API response provides an icon code like "01d" for clear sky
        const iconCode = this.weatherData.weather[0].icon;
        return `https://openweathermap.org/img/w/${iconCode}.png`;
      }
      return ""; // Return an empty string if no weather data or icon code is available
    },
  },
  methods: {
    async fetchWeatherData() {
      const targetCity = this.city || this.defaultCity;
      try {
        const response = await axios.get(
          `https://api.openweathermap.org/data/2.5/weather?q=${targetCity}&appid=${this.apiKey}`
        );
        this.weatherData = response.data;
      } catch (error) {
        console.error(error);
      }
    },
  },
  watch: {
    city: "fetchWeatherData",
  },
  created() {
    this.fetchWeatherData();
  },
};
</script>
