<template>
  <div class="wrapper">
    <LeftPanel
      @send-id="sendId"
      :data="weather.consolidated_weather[0]"
      :location="weather.title"
      :tempStatus="tempActive"
    />
    <RightPanel :data="weather" :tempStatus="tempActive" @temp-btn-click="toggleTemp"/>
  </div>
</template>

<script>
import LeftPanel from "./components/LeftPanel";
import RightPanel from "./components/RightPanel";

export default {
  name: "App",
  components: {
    LeftPanel,
    RightPanel,
  },
  data() {
    return {
      weather: [],
      tempActive: true,
      locID: 2487956,
    };
  },
  emits:['temp-btn-click'],
  methods: {
    async sendId(id) {
      this.locID = await id;
      console.log("loc", this.locID);
      this.weather = await this.fetchWeather(id);
    },
    async fetchWeather(id) {
      const apiFetchUrl = "https://api.allorigins.win/raw?url=";
      const apiUrl = "https://www.metaweather.com/api/location/";
      let url = `${apiFetchUrl}${apiUrl}${id}`;
      let res = await fetch(`${url}`);
      let data = await res.json();
      return data;
    },
    toggleTemp(){
      this.tempActive = !this.tempActive
      console.log('hi')
    },
  },
  async created() {
    this.weather = await this.fetchWeather(this.locID);
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Raleway:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  font-size: 62.5%;
  font-family: "Raleway", sans-serif;
}

.wrapper {
  width: 100%;
  height: 100vh;
  position: relative;
  display: flex;
}
@media screen and (max-width: 1200px) and (min-width: 993px) {
}

@media screen and (max-width: 992px) and (min-width: 769px) {
  .wrapper {
    flex-direction: column;
    height: unset;
  }
}
@media screen and (max-width: 768px) and (min-width: 481px) {
  .wrapper {
    flex-direction: column;
    height: unset;
  }
}

@media screen and (max-width: 480px) {
  .wrapper {
    flex-direction: column;
    height: unset;
  }
}
</style>
