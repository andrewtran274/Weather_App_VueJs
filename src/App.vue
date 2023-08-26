<template>
  <div class="container">
    <h1 class="title">Weather App</h1>
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

<style scoped>
.container {
  width: 400px;
  max-width: calc(100% - 50px);
  height: max-content;
  background-color: #fff;
  padding: 20px;
  border-radius: 100px;
  text-align: center;
  box-shadow: 0px 3px 3px 0px rgba(0, 0, 0, 0.12),
    0px 3px 6px 0px rgba(0, 0, 0, 0.22), 0px 5px 10px 0px rgba(0, 0, 0, 0.2),
    0px 8px 12px 1px rgba(0, 0, 0, 0.19);
  border: 1px solid rgba(0, 0, 0, 0.03);
  border-radius: 6px;
}

.title {
  font-size: 40px;
  font-weight: 400;
  margin-bottom: 20px;
}
</style>
