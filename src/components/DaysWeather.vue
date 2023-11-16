<template>
  <div class="days-tab text-center ">
    <div v-if="Loading" class="Loading">Loading...</div>
   <div v-else >
    <ul class="p-0" style=" display:flex; align-items: center; justify-content: center;" >
      <li v-for="day in forecast"  :key="day.date" class="li_active">
        <py class="py-3"><img :src="day.iconUrl"></py>
        <py class="py-3">{{ getDayName(day.date) }}</py>
        <py class="py-3">{{ day.temperature }}&deg;C</py>
      </li>
    </ul>
   </div>
    
  </div>
</template>

<script>
import axios from 'axios';
import moment from 'moment';
export default {
  name: "DaysWeather",
  props:["cityname"],
  data() {
    return {
      forecast: [],
      Loading: true,
      iconUrl: null,
    };
  },
  methods: {
  async  fetchWeaterData(){
  const  apiKey = '606b6c417293fdd930fb719770ec7cbe';
  const city = this.cityname;
  const apiUrl = `https://api.openweathermap.org/data/2.5/forecast?q=${city}&units=metric&appid=${apiKey}`;
  await axios.get(apiUrl).then(Response => {
    const forecastData = Response.data.list;
    const filterData = forecastData.map(item =>{
      return{
        date: moment(item.dt_txt.split(' ')[0]),
        temperature: Math.round(item.main.temp),
        description: item.weather[0].description,
          iconUrl: `https://api.openweathermap.org/img/w/${item.weather[0].icon}.png`,
      };
    }).reduce((acc,item) => {
      if(!acc.some(day => day.date.isSame(item.date, 'day'))){
      acc.push(item)
      }
        return acc;
    }, []).slice(1,5);
    console.log(filterData, 'working');
    this.forecast = filterData
    this.Loading = false;
  }).catch(error => {
    console.log('error fetching weater data', error);
    this.Loading = false;
  });
    },
    getDayName(date){
return date.format('ddd')
    }
  },
  mounted(){
    this.fetchWeaterData()
  }
};
</script>

<style>
.days-tab{
  width: 90%;
  /* box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2), 0 6px 20px 0 , rgba(0,0,0,0.19) !important; */
  box-shadow: 0px 10px 20px #cccccc2c !important;
  border-radius: 20px;
  margin: auto;
  /* display: flex;
  align-items: center; */
  
}

.Loading{
  color: #fff;
}


.li_active{
  background: #253d5c;
  color: #222831;
  border-radius: 10px;
  margin: 0.5rem;
  color: #fff;
  display: flex;
  flex-direction: column;
  width: 100px;;
}


.li_active:hover{
  transform: scale(1.1);
  transition: all 0.1s ease;
}
</style>
