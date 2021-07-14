<template>
  <div id="app">
    <main>
      <div class="search-box">
        <h1>Nithin's Weather Report Checker</h1>
        <input type="text" @keypress="fetchDetails" name="" id="" v-model="query" class="search-bar" placeholder="Search...">
      </div>
      <div class="weather-wrap" v-if="typeof weather.main != 'undefined' ">
        <div class="location-box">
          <div class="location">{{weather.name}},{{weather.sys.country}}</div>
          <div class="date">{{dateBuilder()}}</div>
        </div>
        <div class="weather-box">
          <div class="temp">{{weather.main.temp}}&#8451;</div>
          <div class="weather">{{weather.weather[0].main}}</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
let x = process.env.NITHIN;
console.log(x);
export default {
  name: 'App',
  data()
  {
     return{
          api_key: '1a946dc3c3c0d62f69cd117984be1257' ,
          url_base:'http://api.openweathermap.org/data/2.5/',
          query: '',
          weather : {}
       }
  } ,
  methods: {
      fetchDetails(e)
      {
          if(e.key == 'Enter')
          {
            fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
            .then(res=> {return res.json()} )
            .then(this.setResults)
          }
      },
      setResults(results)
      {
          console.log(results);
          this.weather = results;
          console.log(this.weather);
      },
      dateBuilder()
      {
        let d = new Date();
        let months = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'];
        let days = ['Sunday','Monday','Tuesday','Wednesday','Thursday','Friday','Saturday'];
        let day = days[d.getDay()]
        let date= d.getDate()
        let month = months[d.getMonth()]
        let year = d.getFullYear()
        return `${day} ${date} ${month} ${year}`
      }
  }
}
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Gugi&display=swap");
  *{
    margin:0;
    padding:0;
    box-sizing: border-box;
  }
  body
  {
    font-family: 'montserrat',sans-serif;
  }
  #app
  {
    background-image: url('./assets/logo.jpg') ;
    background-size: cover;
    transition: 0.4s;
  }
  main
  {
    min-height: 100vh;
    padding: 35px;
  }
  .search-box
  {
    width: 100%;
    margin-bottom: 30px;
  }
  .search-box .search-bar:focus
  {
    background-color: rgba(255,255,255,0.65);
    border-radius: 16px 0px 16px 0px;
    color: black;
    font-family: Gugi;
  }
  .search-box .search-bar
  {
    display: block;
    width: 100%;
    padding: 15px;
    font-size: 20px;
    color: gray;
    appearance: none;
    border: none;
    outline: none;
    background-color: rgba(255,255,255, 0.15);
    border-radius: 0px 16px 0px 16px;
  }
  h1
  {
    color:#202020;
    text-align: center;
    font-family: Gugi;
  }
  ::placeholder
  {
    color:white;
  }
  .location-box .location
  {
    font-family: Gugi;
    color: white;
    font-size: 32px;
    font-weight: 500;
    text-align: center;
    text-shadow: none;
  }
  .location-box .date
  {
    color: #fff;
    font-size: 20px;
    font-weight: 300px;
    font-style:italic;
    text-align:center;
  }
  .weather-box 
  {
    text-align: center;
  }
  .weather-box .temp
  {
    display: inline-block;
    padding: 10px 25px;
    color: white;
    font-size: 102px;
    font-weight: 900;
    text-shadow: 3px 6px rgba(0,0,0,0.25);
    background-color: rgba(255,255,255, 0.25);
    border-radius: 16px;
    margin: 30px 0px;
  }
  .weather-box .weather
  {
      color: white;
      font-size: 48px;
      font-weight: 700;
      font-style: oblique;
      font-family: Gugi;
  }
  .weather-wrap
  {
    background-color: rgba(0,0,0,0.25);
  }
  @media screen and (max-width: 600px) {
  h1{
    font-size: 30px;
    float: left;
    margin-bottom: 20px;
  }
  .weather-box .temp
  {
    font-size: 50px;
  }
}
</style>
