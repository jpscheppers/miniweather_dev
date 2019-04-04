<template>
  <div id="app">
        
    <div class="container">
      <div class="row">
        <div class="col-sm">
        </div>
        <div class="col-sm-4">
          
        </div>
        <div class="col-sm">
        </div>
        </div>
        <div class="container">
        <div class="row">
        <div class="col-sm">
        </div>
        <div class="col-sm-5 mainScreen">
          <h1 class="whiteFont">miniWeather</h1>
            <div class="input-group">
            <input @submit.prevent="getWeather()" v-model="inputdata" v-on:keyup.enter="getWeather()" type="text" class="form-control" aria-describedby="browsecity" placeholder="Enter city">
            <span class="input-group-btn"><button type="submit" v-on:click="getWeather" class="btn btn-default">Get weather now!</button></span>
            </div>
          <div><p>City: {{city}}, {{country}}</p></div>
          <div><p>{{currentTemp}}</p></div>
          <div><p>{{overcast}}</p><img v-bind:src="icon" alt="icon"></div>
          <img src="./assets/img/01d.png"/>
          <div><p>{{icon}}</p></div>
          <div><p>Wind {{wind}}
            <span v-if="winddir > 337.5 && winddir <= 22.5">N</span>
            <span v-else-if="winddir > 22.5 && winddir<= 67.5">NE</span>
            <span v-else-if="winddir > 67.5 && winddir<= 112.5">E</span>
            <span v-else-if="winddir > 112.5 && winddir<= 157.5">SE</span>
            <span v-else-if="winddir > 157.5 && winddir<= 202.5">S</span>
            <span v-else-if="winddir > 202.5 && winddir<= 247.5">SW</span>
            <span v-else-if="winddir > 247.5 && winddir<= 292.5">W</span>
            <span v-else-if="winddir > 292.5 && winddir<= 337.5">NW</span>
            </p>
          </div>
          <div><p>Humidity {{humidity}}</p></div>
          <div><p>{{pressure}}</p></div>
        </div>
        <div class="col-sm">
        </div>
      </div>
    </div>
  </div>
  </div>
</template>
<script>
// import HelloWorld from './components/HelloWorld.vue'
import axios from 'axios'
export default {
  name: 'app',
  components: {
  },
  data() {
    return {
      resp: null,
      inputdata: '',
      city:'',
      country:'',
      currentTemp: '',
      minTemp:'',
      maxTemp:'',
      sunrise:'',
      sunset:'',
      pressure:'',
      humidity:'',
      wind:'',
      winddir:'',
      overcast:'',
      icon:''
    }
  },
  methods:{
    getWeather(){
      let url=`http://api.openweathermap.org/data/2.5/weather?q=${this.inputdata}&units=metric&lang=en&APPID=fead09aadf4f208af0a79233ca98019d`;
      axios
        .get(url)
        .then(response => {
          this.resp = response.data;
          this.currentTemp = this.resp.main.temp + "°C";
          this.minTemp = this.resp.main.temp_min;
          this.maxTemp = this.resp.main.temp_max;
          this.pressure = this.resp.main.pressure + "mbar";
          this.humidity = this.resp.main.humidity + "%";
          this.wind = this.resp.wind.speed + "m/s";
          this.winddir = this.resp.wind.deg;
          this.overcast = this.resp.weather[0].description;
          this.city = this.resp.name;
          this.country = this.resp.sys.country;
          this.icon = "./assets/img/" + this.resp.weather[0].icon + ".png";
          this.sunrise = new Date(this.resp.sys.sunrise*1000).toLocaleTimeString("fr-FR").slice(0.4);
          this.sunset = new Date(this.resp.sys.sunset*1000).toLocaleTimeString("fr-FR").slice(0.4);
        })
      .catch(error => {
        throw(error);
      });
    },
    beforeMonth(){
      this.getWeather();
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.mainScreen {
  background-image: url(./assets/img/PremGurusamyDay-min.png);
  background-size: cover;
  border-radius: 5%;
}
h1, p {
  color:#fff;
}
</style>
