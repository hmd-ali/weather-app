<template>
  <div class="wrapper">
    <PreLoader />
    <LeftPanel
      @send-id="sendId"
      :data="weather.consolidated_weather[0] || [] "
      :location="weather.title"
      :tempStatus="tempActive"
    />
    <RightPanel :data="weather" :tempStatus="tempActive" @temp-btn-click="toggleTemp"/>
  </div>
</template>

<script>
import PreLoader from "./components/PreLoader.vue";
import LeftPanel from "./components/LeftPanel";
import RightPanel from "./components/RightPanel";


export default {
  name: "App",
  components: {
    LeftPanel,
    RightPanel,
    PreLoader,
  },
  data() {
    return {
      weather: {"consolidated_weather":[{"id":6565636898553856,"weather_state_name":"Clear","weather_state_abbr":"c","wind_direction_compass":"W","created":"2021-10-01T21:59:16.560012Z","applicable_date":"2021-10-01","min_temp":13.74,"max_temp":27.4,"the_temp":24.240000000000002,"wind_speed":3.462186158750232,"wind_direction":272.3332279826744,"air_pressure":1015.0,"humidity":52,"visibility":14.302100731726716,"predictability":68},{"id":6395094644031488,"weather_state_name":"Light Cloud","weather_state_abbr":"lc","wind_direction_compass":"W","created":"2021-10-01T21:59:19.248934Z","applicable_date":"2021-10-02","min_temp":13.395,"max_temp":23.865000000000002,"the_temp":24.275,"wind_speed":3.061946598244916,"wind_direction":260.188653928351,"air_pressure":1016.0,"humidity":52,"visibility":14.523308876163206,"predictability":70},{"id":4759927580000256,"weather_state_name":"Light Cloud","weather_state_abbr":"lc","wind_direction_compass":"WSW","created":"2021-10-01T21:59:22.162913Z","applicable_date":"2021-10-03","min_temp":14.055,"max_temp":23.925,"the_temp":24.21,"wind_speed":3.0967044679922586,"wind_direction":253.49656068132413,"air_pressure":1014.5,"humidity":54,"visibility":14.077785731329039,"predictability":70},{"id":6187369062465536,"weather_state_name":"Light Cloud","weather_state_abbr":"lc","wind_direction_compass":"WSW","created":"2021-10-01T21:59:25.248404Z","applicable_date":"2021-10-04","min_temp":13.47,"max_temp":20.975,"the_temp":22.305,"wind_speed":3.816738456069885,"wind_direction":251.48605044555177,"air_pressure":1014.0,"humidity":58,"visibility":14.184040205201622,"predictability":70},{"id":5080611489316864,"weather_state_name":"Heavy Cloud","weather_state_abbr":"hc","wind_direction_compass":"WSW","created":"2021-10-01T21:59:28.174586Z","applicable_date":"2021-10-05","min_temp":13.045,"max_temp":17.535,"the_temp":17.42,"wind_speed":5.840833224616241,"wind_direction":255.12476263605498,"air_pressure":1014.5,"humidity":77,"visibility":13.007784538296349,"predictability":71},{"id":5322877533421568,"weather_state_name":"Heavy Cloud","weather_state_abbr":"hc","wind_direction_compass":"W","created":"2021-10-01T21:59:31.250687Z","applicable_date":"2021-10-06","min_temp":12.135,"max_temp":15.94,"the_temp":14.36,"wind_speed":7.066784975741669,"wind_direction":271.5,"air_pressure":1016.0,"humidity":80,"visibility":9.999726596675416,"predictability":71}],"time":"2021-10-01T15:44:35.354175-07:00","sun_rise":"2021-10-01T07:05:36.921701-07:00","sun_set":"2021-10-01T18:53:37.522590-07:00","timezone_name":"LMT","parent":{"title":"California","location_type":"Region / State / Province","woeid":2347563,"latt_long":"37.271881,-119.270233"},"sources":[{"title":"BBC","slug":"bbc","url":"http://www.bbc.co.uk/weather/","crawl_rate":360},{"title":"Forecast.io","slug":"forecast-io","url":"http://forecast.io/","crawl_rate":480},{"title":"HAMweather","slug":"hamweather","url":"http://www.hamweather.com/","crawl_rate":360},{"title":"Met Office","slug":"met-office","url":"http://www.metoffice.gov.uk/","crawl_rate":180},{"title":"OpenWeatherMap","slug":"openweathermap","url":"http://openweathermap.org/","crawl_rate":360},{"title":"Weather Underground","slug":"wunderground","url":"https://www.wunderground.com/?apiref=fc30dc3cd224e19b","crawl_rate":720},{"title":"World Weather Online","slug":"world-weather-online","url":"http://www.worldweatheronline.com/","crawl_rate":360}],"title":"San Francisco","location_type":"City","woeid":2487956,"latt_long":"37.777119, -122.41964","timezone":"US/Pacific"},
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
  watch(){
    this.weather = (newWeaher) =>{
      this.weather = newWeaher
    }
  }
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
