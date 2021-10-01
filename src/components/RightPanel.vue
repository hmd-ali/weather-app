<template>
  <div class="container">
    <div class="temp-button-container">
      <TempButton
        text="&deg;C"
        :tempStatus="tempStatus"
        @temp-btn-click="tempClick"
      />
      <TempButton
        text="&deg;F"
        :tempStatus="!tempStatus"
        @temp-btn-click="tempClick"
      />
    </div>
    <div class="weather-data">
      <WeatherDay
        :data="data.consolidated_weather[1]"
        day="Tomorrow"
        :tempStatus="tempStatus"
      />
      <WeatherDay
        :data="data.consolidated_weather[2]"
        :day="getDateString(data.consolidated_weather[2].applicable_date)"
        :tempStatus="tempStatus"
      />
      <WeatherDay
        :data="data.consolidated_weather[3]"
        :day="getDateString(data.consolidated_weather[3].applicable_date)"
        :tempStatus="tempStatus"
      />
      <WeatherDay
        :data="data.consolidated_weather[4]"
        :day="getDateString(data.consolidated_weather[4].applicable_date)"
        :tempStatus="tempStatus"
      />
      <WeatherDay
        :data="data.consolidated_weather[5]"
        :day="getDateString(data.consolidated_weather[5].applicable_date)"
        :tempStatus="tempStatus"
      />
    </div>
    <div class="highlights-container">
      <h1>Today's highlights</h1>
      <div class="wind-humidity">
        <Wind :data="data.consolidated_weather[0]" />
        <Humidity :data="data.consolidated_weather[0]" />
      </div>
      <div class="detail-container">
        <VisPress
          text="Visibility"
          units="miles"
          :data="data.consolidated_weather[0].visibility"
        />
        <VisPress
          text="Air Pressure"
          units="mb"
          :data="data.consolidated_weather[0].air_pressure"
        />
      </div>
    </div>
    <footer>
      <p>created by <span>Ali Hammmoud</span></p>
    </footer>
  </div>
</template>

<script>
import WeatherDay from "./WeatherDay";
import TempButton from "./TempButton";
import VisPress from "./VisPress";
import Wind from "./Wind";
import Humidity from "./Humidity";

export default {
  name: "RightPanel",
  components: {
    TempButton,
    WeatherDay,
    VisPress,
    Wind,
    Humidity,
  },
  props: {
    data: Object,
    tempStatus: Boolean,
  },
  emits: ["temp-btn-click"],
  methods: {
    getDateString(mydate) {
      const date = new Date(mydate);
      const months = [
        "Jan",
        "Feb",
        "Mar",
        "Apr",
        "May",
        "Jun",
        "Jul",
        "Aug",
        "Sep",
        "Oct",
        "Now",
        "Dec",
      ];
      const days = ["Sun.", "Mon.", "Tue.", "Wed.", "Thu.", "Fri.", "Sat."];
      let day = days[date.getDay()];
      let weekDay = date.getDate();
      let month = months[date.getMonth()];

      return day + " " + weekDay + " " + month;
    },
    tempClick() {
      this.$emit("temp-btn-click");
    },
  },
};
</script>

<style scoped>
.container {
  position: relative;
  width: 67%;
  height: 100vh;
  min-height: 840px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  background: #100e1d;
}
.temp-button-container {
  position: relative;
  width: 100%;
  padding: 2rem 2rem;
  display: flex;
  justify-content: flex-end;
}

.weather-data {
  position: relative;
  width: 100%;
  max-width: 1000px;
  padding: 1rem 10rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.highlights-container {
  position: relative;
  width: 100%;
  max-width: 1000px;
  padding: 1rem 10rem;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  color: #e7e7eb;
}

.highlights-container h1 {
  width: 100%;
}
.highlights-container .wind-humidity {
  position: relative;
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 3rem;
}
.highlights-container .detail-container {
  position: relative;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-top: 3rem;
}
footer {
  width: 100%;
  color: #a09fb1;
  font-size: 1.4rem;
  text-align: center;
  padding: 2rem 2rem;
}

footer span {
  font-weight: 700;
}
@media screen and (max-width: 1200px) and (min-width: 993px) {
  .weather-data {
    padding: 1rem 2rem;
  }
  .highlights-container {
    padding: 1rem 2rem;
  }
  .highlights-container .wind-humidity {
    display: flex;
    flex-direction: row;
    justify-content: space-evenly;
  }
  .highlights-container .detail-container {
    display: flex;
    flex-direction: row;
    justify-content: space-evenly;
  }
}

@media screen and (max-width: 992px) and (min-width: 769px) {
  .container {
    padding-top: 4rem;
    min-width: 100%;
    display: flex;
    flex-direction: column;
    height: auto;
  }
  .temp-button-container {
    display: none;
  }
  .weather-data {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    padding: unset;
  }
  .highlights-container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 100%;
    padding: 2rem 1rem 2rem 1rem;
  }
  .highlights-container h1 {
    text-align: center;
  }
  .highlights-container .wind-humidity {
    display: flex;
    flex-direction: row;
    justify-content: space-evenly;
  }
  .highlights-container .detail-container {
    display: flex;
    flex-direction: row;
    justify-content: space-evenly;
  }
}

@media screen and (max-width: 768px) and (min-width: 481px) {
  .container {
    padding-top: 4rem;
    min-width: 100%;
    display: flex;
    flex-direction: column;
    height: auto;
  }
  .temp-button-container {
    display: none;
  }
  .weather-data {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    padding: unset;
  }
  .highlights-container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 100%;
    padding: 2rem 0.5rem 2rem 0.5rem;
  }
  .highlights-container h1 {
    text-align: center;
  }
  .highlights-container .wind-humidity {
    display: flex;
    flex-direction: column;
    gap: 3rem;
  }
  .highlights-container .detail-container {
    display: flex;
    flex-direction: column;
    gap: 3rem;
  }
}
@media screen and (max-width: 480px) {
  .container {
    padding-top: 4rem;
    min-width: 100%;
    display: flex;
    flex-direction: column;
    height: auto;
  }
  .temp-button-container {
    display: none;
  }
  .weather-data {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    padding: unset;
  }
  .highlights-container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 100%;
    padding: 2rem 0.5rem 2rem 0.5rem;
  }
  .highlights-container h1 {
    text-align: center;
  }
  .highlights-container .wind-humidity {
    display: flex;
    flex-direction: column;
    gap: 3rem;
  }
  .highlights-container .detail-container {
    display: flex;
    flex-direction: column;
    gap: 3rem;
  }
}
</style>