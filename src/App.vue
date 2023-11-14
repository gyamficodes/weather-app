<template>
  <div id="app" >
    <div class="header container h-100 p-5">
      <h1 class="mb-5">Weather app</h1>
      <div class="d-flex justify-content-center h-100">
        <div class="w-50 mx2">
          <input
            type="text"
            v-model="city"
            placeholder="Enter a city"
            class="form-control"
          />
        </div>
        <button @click="searchWeather" class="btn-search btn btn-primary">
          search <i class="fas fa-search"></i>
        </button>
      </div>
    </div>
    <weather :city="city" v-if="showWeather"></weather>
  </div>
</template>

<script>
import Weather from "./components/Weather.vue";
export default {
  name: "App",
  components: {
    Weather,
  },
  data() {
    return {
      city: "",
      showWeather: false,
    };
  },
  methods: {
    async searchWeather() {
      this.showWeather = false;
      await this.$nextTick();
      this.showWeather = true;
    },
  },
};
</script>

<style lang="css">
body {
  background: #121212 !important;

}

.header {
  color: #fff;
  background-color: #212730;
  border-radius: 20px;
  text-align: center;
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
  margin-top: 5rem;
}
.btn-search {
  background: linear-gradient(to right, cyan, magenta);
}
</style>
