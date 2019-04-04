<template>
  <div id="app">
    <h1>O shit waddup</h1>
    <form @submit.prevent="getWeather()">
      <div class="row">
        <div class="offset-md-3 col-md-6">
          <div class="form-group">
            <input v-model="inputdata" type="text" class="form-control" aria-describedby="browsecity" placeholder="Enter city">
          </div>
        </div>
      </div>
      <div class="row">
        <div class="offset-md-2 col-md-8">
          <div class="row">
            <div class="col-md-12 border border-dark">
              <HelloWorld/>
            </div>
          </div>
          <div class="row">
            <div class="offset-md-1 col-md-2 border border-dark"><p></p></div>
            <div class="col-md-2 border border-dark"><p>{{inputdata}}</p></div>
            <div class="col-md-2 border border-dark"><p>{{currentTemp}}</p></div>
            <div class="col-md-2 border border-dark"><p>{{icon}}</p></div>
            <div class="col-md-2 border border-dark"><img src="assets/img/01.svg" alt="icon"></div>
          </div>
        </div>
      </div>
    </form>
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
      inputdata: "",
      currentTemp: "",
      minTemp:"",
      maxTemp:"",
      sunrise:"",
      sunset:"",
      pressure:"",
      humidity:"",
      wind:"",
      overcast:"",
      icon:""
    }
  },
  methods:{
    getWeather(){
      let url=`http://api.openweathermap.org/data/2.5/weather?q=${this.inputdata}&units=metric&APPID=fead09aadf4f208af0a79233ca98019d`;
      axios
        .get(url)
        .then(response => {
          this.resp = response.data;
          this.currentTemp = this.resp.main.temp;
          this.minTemp = this.resp.main.temp_min;
          this.maxTemp = this.resp.main.temp_max;
          this.pressure = this.resp.main.pressure;
          this.humidity = this.resp.main.humidity + "%";
          this.wind = this.resp.wind.speed + "m/s";
          this.overcast = this.resp.weather[0].description;
          this.icon = "/assets/img/" + this.resp.weather[0].icon.slice(0,2) + ".png";
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
</style>
