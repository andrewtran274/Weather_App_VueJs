<template>
  <div>
    <h1>Weather App</h1>
    <CityInput @city-changed="updateCity" />
    <Weather :apiKey="apiKey" :city="city" />
  </div>
</template>

<script>
import CityInput from "./components/CityInput.vue";
import Weather from "./components/Weather.vue";

export default {
  components: {
    CityInput,
    Weather,
  },
  data() {
    return {
      apiKey: "329471f2ef8fe7164fc7c314bffbda4a",
      city: "London",
    };
  },
  methods: {
    updateCity(newCity) {
      this.city = newCity;
    },
  },
};
</script>

<style lang="scss" scoped></style>
