<template>
  <div class="weather container">
    <img class="weather-icon" :src="icon" :alt="description" />
    &nbsp;
    <span id="area" class>
      <img class="weather-unit" src="../../static/img/icons/location.png" alt />
      {{city}}
    </span> &nbsp;
    <span class>
      <img class="weather-unit" src="../../static/img/icons/dt.png" alt />
      {{dt}}
    </span>
    <br />&nbsp;
    <span class>
      <img class="weather-unit" src="../../static/img/icons/sunrise.png" alt />
      {{sunrise}}
    </span> &nbsp;
    <span class>
      <img class="weather-unit" src="../../static/img/icons/sunset.png" alt />
      {{sunset}}
    </span>
    &nbsp;
    <span class>
      <img class="weather-unit" src="../../static/img/icons/temp.png" alt />
      {{currentTemp}}
    </span>
    <br />&nbsp;
    <span class>
      <img class="weather-unit" src="../../static/img/icons/pressure.png" alt />
      {{pressure}}
    </span> &nbsp;
    <span class>
      <img class="weather-unit" src="../../static/img/icons/humidity.png" alt />
      {{humidity}}
    </span> &nbsp;
    <span class>
      <img class="weather-unit" src="../../static/img/icons/windspeed.png" alt="wind icon error" />
      {{wind}}
    </span>
  </div>
</template>

<script>
const API = "https://api.openweathermap.org/data/2.5/weather?units=metric";
const KEY = "&APPID=0ab1cd22e4c10d85a9c380f889155e6b";
import axios from "axios";

export default {
  name: "weather",
  data() {
    return {
      city: "",
      dt: "",
      currentTemp: "",
      // minTemp: '',
      // maxTemp: '',
      sunrise: "",
      sunset: "",
      pressure: "",
      humidity: "",
      wind: "",
      description: "",
      icon: "",
      location: ""
    };
  },
  methods: {
    getWeather(url) {
      this.$axios
        .get(url)
        .then(res => {
          // console.log(res.data);
          this.city = res.data.name + "," + res.data.sys.country;
          this.dt = new Date(res.data.dt * 1000)
            .toLocaleTimeString("en-GB")
            .slice(0, 5);
          this.currentTemp = parseInt(res.data.main.temp) + "℃";
          this.pressure = res.data.main.pressure + "hpa";
          this.humidity = res.data.main.humidity + "%";
          this.wind = res.data.wind.speed + "m/s";
          this.description = res.data.weather[0].description;
          this.icon =
            "./static/img/weather/" + res.data.weather[0].icon + ".png";
          // console.log(res.data.weather[0].icon.slice(0, 2));
          // console.log(res.data.weather[0].icon);
          this.sunrise = new Date(res.data.sys.sunrise * 1000)
            .toLocaleTimeString("en-GB")
            .slice(0, 5);
          this.sunset = new Date(res.data.sys.sunset * 1000)
            .toLocaleTimeString("en-GB")
            .slice(0, 5);
          // this.location =
          //   JSON.stringify(res.data.coord.lon).replace(".", "°") +
          //   "，" +
          //   JSON.stringify(res.data.coord.lat).replace(".", "°");
        })
        .catch(error => {
          console.log(error);
        });
    },
    geolocation() {
      navigator.geolocation.getCurrentPosition(this.buildUrl, this.geoError);
    },
    buildUrl(position) {
      const lat = position.coords.latitude;
      const lon = position.coords.longitude;

      this.getWeather(API + "&lat=" + lat + "&lon=" + lon + KEY);
    },
    geoError(error) {
      this.getWeather(API + "&lat=0&lon=0" + KEY);
    }
  },
  beforeMount() {
    this.geolocation();
  }
};
</script>

<style scoped>
.weather-unit {
  width: 30px;
}
.weather-icon {
  height: 90px;
  float: left;
}
</style>