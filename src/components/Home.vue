<template>
  <div id="ancestor">
   <div class="container-fluid" id="app">
     <div class="row">
       <div id="sidebar" class="col-md-3 col-sm-4 col-xs-12 sidebar">
         <div id="search">
           <input
             id="location-input"
             type="text"
             ref="input"
             placeholder="Location?"
             v-model="cityQuery"
             @keyup.enter="getWeatherInfo"
           >
           <button id="search-btn" @click="getWeatherInfo">
             <img src="../assets/Search.svg" width="24" height="24">
           </button>
         </div>
         <div id="info">
           <img :src="icon">
           <div class="wrapper-left">
             <div id="current-weather" style="display: inline-block">
               {{ temperature }}
               <span>°C</span>
             </div>
             <div id="weather-desc">{{ summary }}</div>
             <div class="temp-max-min">
               <div class="max-desc">
                 <div id="max-detail">
                   <i>▲</i>
                   {{ maxTemp }}
                   <span>°C</span>
                 </div>
               </div>
               <div class="min-desc">
                 <div id="min-detail">
                   <i>▼</i>
                   {{ minTemp }}
                   <span>°C</span>
                 </div>
               </div>
             </div>
           </div>
           <div class="wrapper-right">
             <div class="date-time-info">
               <div id="date-desc">
                 <img src="../assets/calendar.svg" width="20" height="20">
                 {{ timeDate }}
               </div>
             </div>
             <div class="location-info">
               <div id="location-desc">
                 <img
                   src="../assets/location.svg"
                   width="10.83"
                   height="15.83"
                   style="opacity: 0.9;"
                 >
                 {{ location }}
                 <div id="location-detail" class="mt-1">
                   Lat: {{ lat }}
                   <br>
                   Long: {{ lng }}
                 </div>
               </div>
             </div>
           </div>
         </div>
       </div>
       <dashboard-content
         class="col-md-9 col-sm-8 col-xs-12 content"
         id="dashboard-content"
         :highlights="highlights"
         :embedFrame="embedFrame"
       ></dashboard-content>
     </div>
   </div>
 </div>
</template>

<script>
import axios from 'axios'
import Content from './Content.vue'

export default {
  name: 'home',
  components: {
    'dashboard-content': Content
  },
  data () {
    return {
      weatherInfo: '',
      cityName: '',
      windSpeed: '',
      temperature: '',
      humidity: '',
      UVIndex: '',
      icon: 'https://i.ibb.co/7g1rL9r/15-155040-weather-icon-weather.png" alt="15-155040-weather-icon-weather',
      date: '',
      lat: '',
      lng: '',
      maxTemp: '',
      minTemp: '',
      summary: '',
      location: '',
      timeDate: '',
      cityQuery: 'Carlow',
      highlights: {
        windStatus: {
          windSpeed: '',
          windDegrees: '',
          gust: ''
        }
      },
      embedFrame: {
        src: ''
      }
    }
  },
  created () {
    this.getWeatherInfo()
    // console.log("API key=" + process.env.VUE_APP_OPEN_WEATHER_MAP_API_KEY)
  },
  methods: {
    getWeatherInfo() {
      const url = `https://api.openweathermap.org/data/2.5/weather?q=${this.cityQuery}&appid=79eca4e1208fe4818f31afd082716197&units=metric`;
      axios.get(url).then(res => {
        let data = res.data
        this.weatherInfo = data
        console.log(this.weatherInfo)
        this.cityName = data.name
        this.temperature = Math.ceil(data.main.temp)
        this.highlights.windStatus.windSpeed = data.wind.speed
        this.highlights.windStatus.gust = data.wind.gust
        this.highlights.windStatus.windDegrees = data.wind.deg
        this.humidity = data.main.humidity + "%"
        this.lat = data.coord.lat
        this.lng = data.coord.lon
        this.maxTemp = Math.ceil(data.main.temp_max)
        this.minTemp= Math.ceil(data.main.temp_min)
        this.summary = data.weather[0].description
        this.location = this.cityName + ", " + data.sys.country
        this.icon = `https://openweathermap.org/img/w/${data.weather[0].icon}.png`
        const timeElapsed = Date.now();
        const today = new Date(timeElapsed);
        this.timeDate = today.toUTCString()
        this.embedFrame.src = `https://maps.google.com/maps?q=${this.cityName}&t=&z=13&ie=UTF8&iwloc=&output=embed`
      }).catch(err => {
        console.log(err)
      })
    }
  }
}
</script>

<style>

</style>
