<template>
  <div id="app">
      <weatherAPI/>
      Hello
        <!-- <img src="assets/images/sunny.svg"> {{overcast}}
        <span class="temperature">{{currentTemp}}°</span><br>
        <span id="temp-values">Min {{minTemp}}° <br> Max {{maxTemp}}°</span>
  
      <div id="info">
        <img class="icon" :src=icon> {{sunrise}}
        <img class="icon" src="assets/images/sunset.svg"> {{sunset}}
        <img class="icon" src="assets/images/humidity.svg"> {{humidity}}
        <img class="icon" src="assets/images/pressure.svg"> {{pressure}}
        <img class="icon" src="assets/images/wind.svg"> {{wind}}
      </div> -->
  </div>
</template>

<script>
import weatherAPI from './components/weatherAPI.vue'


export default {
  name: 'app',
  components: {
    weatherAPI
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smimport './plugins/bootstrap-vue'
sed;
  -moz-osx-font-simport './plugins/bootstrap-vue'
le;
  text-align: cenimport './plugins/bootstrap-vue'

  color: #2c3e50;import './plugins/bootstrap-vue'

  margin-top: 60px;
}
</style>
