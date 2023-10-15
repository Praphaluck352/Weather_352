<script setup>
import { RouterLink } from 'vue-router';
import { ref, watchEffect } from "vue";
import axios from "axios";
import { useWeatherStore } from '@/stores/weather';

const latitude = ref('18.742674409855212'); 
const longitude = ref('97.90419146749545'); 
const weatherStore = useWeatherStore();

watchEffect(() => {
  if (latitude.value && longitude.value) {
    showWeatherData();
  }
});

function WeatherData(url) {
  axios
    .get(url)
    .then((response) => {
      weatherStore.weatherData = response.data;
    })
    .catch((err) => {
      console.error(err);
    });
}

function showWeatherData() {
  const apiUrl = 'https://api.openweathermap.org/data/2.5/forecast';
  const apiKey = '4546b80f7b7b5d308f95442db543cb15';
  const lang = 'th';
  const units = 'metric';
  const url = `${apiUrl}?lat=${latitude.value}&lon=${longitude.value}&appid=${apiKey}&units=${units}&lang=${lang}`;
  WeatherData(url);
}



</script>

<template>
    <div class="frameoutline">
        <div class="frame">
            <div class="card text-center mb-3 mt-4" style="width: 80vw; margin: auto;  background-color:  rgba(255, 255, 255,0.8 );">
                <div class="card-body">
                    <img src="@/assets/weatherMain.png" alt="cardimg" class="mb-3 mt-3" style="width: 30%;">
                    <h3 class="card-title">ค้นหาพยากรณ์อากาศ</h3>
                    <div class="inputframe">
                        <div class="input-group" style="width: 70%; margin: auto;">
                            <span class="input-group-text">ละติจูดและลองติจูด</span>
                            <input type="text" aria-label="latitude" class="form-control" id="lat" v-model="latitude" placeholder="ลติจูด">
                            <input type="text" aria-label="longitude" class="form-control" id="long" v-model="longitude" placeholder="ลองติจูด">
                        </div>
                    </div>
                    
                    <RouterLink to="/weather" class="btn btn-success mt-2 mb-2" style="width: 50%;">ค้นหา</RouterLink>
                </div>
            </div>
        </div>
    </div>

    <footer class="d-flex flex-wrap justify-content-between align-items-center py-3  border-top" style="background-color: rgba(148, 147, 147, 0.4);">
      <div class="col-md-4 d-flex align-items-center">
        <RouterLink to="/" class="mb-3 me-2 mb-md-0 text-body-secondary text-decoration-none lh-1">
          <svg class="bi" width="30" height="24"></svg>
        </RouterLink>
        <span class="mb-3 mb-md-0 text-body-secondary">praphaluck thitimanokun 352</span>
      </div>

    </footer>
</template>

<script>



  


</script>



<style scoped>

body{
    margin: 0%;
    padding: 0%;
}

.frameoutline{
height: 100vh;
background-color: transparent;
}

.frame{
    display: flex;
    background-color: transparent;
}

.inputframe{
    display: flex;
}

</style>