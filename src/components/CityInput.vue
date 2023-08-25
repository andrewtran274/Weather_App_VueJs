<!-- src/components/CityInput.vue -->
<template>
  <form @submit.prevent="handleSubmit">
    <input type="text" v-model="city" placeholder="Enter city name" />
    <button type="submit">Get Weather</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      city: "",
    };
  },
  methods: {
    handleSubmit() {
      this.$emit("city-changed", this.city);
    },
  },
};
</script>
