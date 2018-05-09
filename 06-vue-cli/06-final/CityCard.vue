<template>
  <div class="card">
    <div class="card-body">
      <h5 class="card-title">{{ cityName }}</h5>
      <h6 class="card-subtitle mb-2 text-muted">Now: {{ tempF }}&deg; - {{ weatherDesc }}</h6>
      <button type="button" class="btn btn-primary" v-on:click="toggleForecast">{{showForecast ? 'Hide' : 'Show'}} Forecast</button>
      <div v-if="showForecast">
        <div class="card-text">
          <p>Five-day Forecast (avg: {{ fiveDayAverageTemp }}&deg;)</p>
          <p v-for="forecast in forecastFiveDays" :key="forecast.timestamp">
            <b>{{ forecast.temp }}&deg;</b>
            <br />
            <em>{{ forecast.weatherDesc }}</em>
            <br />
            <small>{{ forecast.timestamp }}</small>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    cityName: {
      type: String,
      required: true
    },
    tempF: {
      type: String,
      required: true
    },
    weatherDesc: {
      type: String,
      required: true
    },
    fiveDayAverageTemp: {
      type: Number,
      required: true
    },
    forecastFiveDays: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      showForecast: false
    };
  },
  methods: {
    toggleForecast() {
      this.showForecast = !this.showForecast;
    }
  }
};
</script>

<style scoped>

</style>