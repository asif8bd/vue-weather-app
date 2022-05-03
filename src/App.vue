<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    <div class="container d-flex justify-content-center">
      <div class="input-group col-sm-7 input-group">
          <div class="input-group-prepend"> <span class="input-group-text google"><img src="https://img.icons8.com/color/48/000000/google-logo.png"></span> </div> 
          <input type="text" class="form-control" placeholder="Enter a city name.." 
              v-model="query"   @keypress="fetchWeather">
          <div class="input-group-append"> <span class="input-group-text microphone"><img src="https://img.icons8.com/nolan/48/000000/microphone.png"></span> </div>
      </div>
  </div>
    
  <h1 class="btn btn-danger" v-if="typeof weather.message != 'undefined'">Requested {{ weather.message }}! Please try another city.</h1>

  <div class="container-fluid px-1 px-md-4 py-5 mx-auto">
      <div class="row d-flex justify-content-center px-3">
          <div class="card" v-if="typeof weather.main != 'undefined'" :class="weather.main.temp > 16 ? 'warm' : 'cold'">
              <h2 class="ml-auto mr-4 mt-3 mb-0">{{ weather.name }}, {{ weather.sys.country }}</h2>
              <p class="ml-auto mr-4 mb-0 med-font">{{ weather.weather[0].main }}</p>
              <h1 class="ml-auto mr-4 large-font">{{ Math.round(weather.main.temp) }}°c</h1>
              <p class="time-font mb-0 ml-4 mt-auto">{{ weather.time }}</p>
              <p class="date-font ml-4 mb-4">{{ weather.date }}</p>
          </div>
      </div>
  </div>

  </div></template>

<script>

export default {
  name: 'App',
  data () {
    return {
      api_key: '691fb5ebc3836df1cd450f0327875a66',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      msg: 'Welcome to Weather App',
      weather: {}
    }
  },
  methods: {
    fetchWeather (e) {
      if (e.key == "Enter") {
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
          .then(res => {
            return res.json();
          }).then(this.setResults);
      }
    },
    setResults (results) {
      this.weather = results;
      this.weather.time=new Date().toLocaleTimeString('en-US');
      this.weather.date=new Date().toLocaleDateString('en-us', { weekday:"long", year:"numeric", month:"short", day:"numeric"}) 

    },
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}



.container {
    margin-top: 20px;
    margin-bottom: 20px
}

.microphone {
    border-top-right-radius: 32px !important;
    border-bottom-right-radius: 32px !important;
    background-color: #fff
}

.google {
    border-top-left-radius: 32px !important;
    border-bottom-left-radius: 32px !important;
    background-color: #fff
}

.input-group-prepend {
    margin-right: -2px !important
}

.input-group-append {
    margin-left: -2px !important
}

.form-control:focus {
    color: #495057;
    background-color: #fff;
    border-color: #ced4da;
    outline: 0;
    box-shadow: 0 0 0 0 !important
}

.form-control {
    border-right: 0 !important;
    border-left: 0 !important
}

/* Weather CSS*/

body {
    color: #fff;
    overflow-x: hidden;
    height: 100%;
    background-color: #CFD8DC;
    background-repeat: no-repeat
}

.card {
    background-size: cover;
    width: 600px;
    height: 350px;
    border-radius: 20px;
    box-shadow: 0px 8px 16px 4px #9E9E9E;
    margin-top: 10px;
    margin-bottom: 10px;
    color: white;
}

.cold{
      background-image: url("./assets/cold.jpg");
}
.warm{
      background-image: url("./assets/warm.jpg");
}

.time-font {
  text-align: left;
    font-size: 40px
}

.date-font {
   text-align: left;
    font-size: 24px
}

.sm-font {
    font-size: 18px
}

.med-font {
    font-size: 28px
}

.large-font {
    font-size: 60px
}

</style>

