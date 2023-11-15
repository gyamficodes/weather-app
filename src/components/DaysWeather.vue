<template>
  <div class="days-tab text-center ">
    <div class="Loading">Loading...</div>
   <div style=" display:flex; align-items: center; justify-content: center;">
    <ul class="p-0">
      <li class="li_active">
        <py class="py-3">icon</py>
        <py class="py-3">day</py>
        <py class="py-3">12oc</py>
      </li>
    </ul>
    <ul class="p-0">
      <li class="li_active">
        <py class="py-3">icon</py>
        <py class="py-3">day</py>
        <py class="py-3">12oc</py>
      </li>
    </ul>
    <ul class="p-0">
      <li class="li_active">
        <py class="py-3">icon</py>
        <py class="py-3">day</py>
        <py class="py-3">12oc</py>
      </li>
    </ul>
    <ul class="p-0">
      <li class="li_active">
        <py class="py-3">icon</py>
        <py class="py-3">day</py>
        <py class="py-3">12oc</py>
      </li>
    </ul>
   </div>
    
  </div>
</template>

<script>
export default {
  name: "DaysWeather",
  props:["cityname"],
  data() {
    return {};
  },
  methods: {
  async  fetchWeaterData(){
  const  apiKey = '';
  const city = this.cityname;
  const apiUrl = ``;
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
