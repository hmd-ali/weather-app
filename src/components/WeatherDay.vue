<template>
  <div class="day-container">
    <p class="day">{{ day }}</p>
    <div class="img-container">
      <img
        :src="require(`../assets/${returnSrc(data.weather_state_name)}.png`)"
        alt="state png"
      />
    </div>
    <div class="min-max">
      <p>{{ Math.floor(data.max_temp) }}&deg;C</p>
      <p>{{ Math.floor(data.min_temp) }}&deg;C</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "WeatherDay",
  props: {
    data: Object,
    day: String,
  },
  methods: {
    returnSrc(weatherState) {
      const states = {
        Snow: "Snow",
        Sleet: "Sleet",
        Hail: "Hail",
        Thunderstorm: "Thunderstorm",
        "Heavy Rain": "HeavyRain",
        "Light Rain": "LightRain",
        Showers: "Shower",
        "Heavy Cloud": "HeavyCloud",
        "Light Cloud": "LightCloud",
        Clear: "Clear",
      };
      const state = states[weatherState];
      return state;
    },
  },
};
</script>

<style scoped>
.day-container {
  position: relative;
  width: 120px;
  height: 177px;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  align-items: center;
  background: #1e213a;
  color: #e7e7eb;
}
.day-container p:first-child {
  font-size: 1.6rem;
  font-weight: 500;
}
.img-container {
  position: relative;
  width: 100%;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.img-container img {
  width: 60%;
}
.min-max {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.min-max p {
  display: inline-block;
  margin: 1rem;
  font-size: 1.6rem;
}
.min-max p:last-child {
  color: #a09fb1;
}

.day {
  font-size: 1.2rem;
}

@media screen and (max-width: 1200px) and (min-width: 993px) {
  .day-container {
    margin: 1%;
  }
}
@media screen and (max-width: 992px) and (min-width: 769px) {
  .day-container {
    margin: 2rem;
  }
}

@media screen and (max-width: 768px) and (min-width: 481px) {
  .day-container {
    margin: 2rem;
  }
}
@media screen and (max-width: 480px) {
  .day-container {
    margin: 1rem;
  }
}
</style>