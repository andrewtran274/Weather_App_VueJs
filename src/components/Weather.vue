<template>
  <div class="weather">
    <img
      v-if="weatherData"
      :src="weatherIconUrl"
      alt="Weather Icon"
      class="weather-img"
    />
    <h1 v-if="weatherData" class="weather-city">{{ weatherData.name }}</h1>
    <p v-if="weatherData" class="temp">{{ weatherData.main.temp }}°F</p>
    <div class="weather-info">
      <div class="element">
        <i class="bx bx-cloud-rain"></i>
        <p v-if="weatherData" class="text">
          Humidity: {{ weatherData.main.humidity }}%
        </p>
      </div>
      <div class="element">
        <i class="bx bx-wind"></i>
        <p v-if="weatherData" class="text">
          Wind: {{ weatherData.wind.speed }}Km/h
        </p>
      </div>
      <p v-if="!weatherData">Enter a city name to get the weather.</p>
    </div>
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
        console.log(response);
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

<style scoped>
.weather-img {
  min-width: 100px;
  /* background-color: red; */
}

.weather-city {
  font-size: 40px;
  font-weight: 400;
}

.temp {
  font-size: 30px;
  font-weight: 300;
  margin-top: 10px;
  margin-bottom: 10px;
}

.weather-info {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.element i {
  font-size: 30px;
  /* font-weight: 200; */
}

.element {
  /* background-color: red; */
}
</style>
