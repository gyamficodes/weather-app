<template>
  <div class="container p-0">
    <div class="d-flex  page">

      <div class="card main-div w-100" >
        <div class="p-3">
          <h2  style="color: #fff;" class="mb-1   day">Today</h2>
          <p class="text-light date mb-0">{{ date }}</p>
          <small style="color: #fff;">{{ time }}</small>
          <h2 class="place" style="color: #fff ;">
            <i class="fas fa-location"></i> {{ name }} <small>{{ country }}</small>
          </h2>
          <div class="temp">
            <h1 style="color: #fff;" class="weather-temp">19&deg;</h1>
            <h2 class="text-light">{{ description }} <img :src="iconUrl" alt=""></h2>
          </div>
        </div>
      </div>

      <div class="card card-2 w-100">
      <table class="m-3">
        <tbody>
          <tr>
            <th>sea level</th>
            <td v-if="sea_level > 0">{{ sea_level }}</td>
            <td v-else>Null</td>
          </tr>
          <tr>
            <th>Humidity</th>
            <td>{{ humidity }}</td>
          </tr>
          <tr>
            <th>wind</th>
            <td>{{ wind }}</td>
          </tr>
        </tbody>
      </table>
      <DaysWeather :cityname="cityname"></DaysWeather>
      <div id="div_form" class="d-flex m-3 justify-content-center">
      <input type="button" value="change location" @click="changeLocation"  class="btn change_btn btn-primary">
      </div>
    </div>
    </div>

  </div>
</template>

<script>
import DaysWeather from './DaysWeather.vue';
import axios from 'axios';
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Weather",
  components: {
    DaysWeather,
  },
  props: ['city'],
  data() {
    return {
    cityname: this.city,
    temperature:null,
    description:null,
    iconUrl:null,
    date:null,
    time:null,
    name: null,
    sea_level: null,
    wind:null,
    country: null,
    humidity:null,
    monthNames: ['January','February','March', 'April','May',"June","July", 'August','September','October','November','December'],
    };
 
  },
  async created() {
    const response = await axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=606b6c417293fdd930fb719770ec7cbe`)
    const weatherData = response.data;
    this.temperature =  Math.round(weatherData.main.temp);
    this.description = weatherData.weather[0].description;
    this.name = weatherData.name;
    this.wind = weatherData.wind.speed;
    this.sea_level = weatherData.main.sea_level;
    this.country = weatherData.sys.country;
    this.humidity = weatherData.main.humidity;
    this.iconUrl = `https://api.openweathermap.org/img/w/${weatherData.weather[0].icon}.png`;
    const d = new Date();

    this.date = d.getDate() + '-' + this.monthNames[d.getMonth()] + '-' + d.getFullYear();
     this.time = d.getHours() + ':' + d.getMinutes() + ':' +  d.getSeconds();
    console.log(weatherData)
    },
  methods: {
  changeLocation(){
    window.location.reload();
  }
  },
};
</script>

<style>
.weather-app{
  margin: 0;
  font-weight: 700;
  font-size: 4em;
}
h1.mb-1.day{
  font-size: 3rem;
  font-weight: 400;
  color: #fff ;

}

.main-div{
  border-radius: 20px;
  color: #fff ;
  background: url(../assets/image/ryan-loughlin-vLZ3ko4cSr0-unsplash.jpg) !important;
  background-repeat: no-repeat ;
  width: 100%;
  height: 100%;
  background-position: center center;
  background-color: rgba(0,0,0,0.5);
  background-blend-mode: overlay;
  background-size: cover;
  
}
.temp{
  position: absolute;
  bottom: 0;
}

.main-div:hover{
  transform: scale(1.1);
  transition: all 0.5s ease-in-out;
  z-index: 1;
}
.card-2{
  background-color: #212730 !important;
  border-radius: 20px !important;
}

.card-details{
  margin-left: 19px;
}

.h1_left{
position: absolute;
bottom: 25px;
left: 16px;
font-size: 3vw;
line-height: 1.2;
}

.h3_left{
  position: absolute;
  left: 16px;
font-size: 2vw;
line-height: 1.2;
}

.h3_left small{
  font-size: 1rem;
}

table{
  position: relative;
  left: 15px;
  border-collapse: separate;
  border-spacing: 15px;
  width: 85%;
  max-width: 85%;
  margin: 0 auto;
}
th,
tr{
  font-size: 18px;
  color: #fff;
}

table,
tr:hover{
  color: red;
}
.change_btn{
  background: linear-gradient(to right, cyan, magenta);
}

</style>
