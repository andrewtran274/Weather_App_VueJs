<!-- src/components/CityInput.vue -->
<template>
  <form @submit.prevent="handleSubmit" class="form">
    <input
      type="text"
      v-model="city"
      placeholder="Enter city name"
      class="form-input"
    />
    <button type="submit" class="btn form-btn">Search</button>
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

<style scoped>
.form {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 20px;
}
.form .form-input {
  flex: 1;
  outline: none;
  border: 1px solid #007b35;
  padding: 10px 20px;
  border-radius: 20px;
  height: 40px;
  line-height: 40px;
  margin-right: 10px;
}

.form .form-btn {
  flex: 0;
  display: block;
  border: none;
  height: 40px;
  line-height: 40px;
  cursor: pointer;
  padding: 0 10px;
  border-radius: 20px;
  border: 1px solid #007b35;
  background-color: #fff;
  transition: all 0.3s;
  font-weight: 500;
}

.form .form-btn:hover {
  background-color: #007b35;
  color: #fff;
}
</style>
