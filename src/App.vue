<template>
  
  
  <div id="app" :class="background">

    <main>
        <div class="elements">
          <div></div>
          <div></div>
          <div></div>
          <div></div>
          <div></div>
          <div></div>
          <div></div>
        </div>
     
      <div class="search-box">
        <input type="text" class="search-bar" 
        placeholder="Search..."
        v-model="searching"
        v-on:keypress="fetchWeather"
        />
      </div>
      <div class="weather-wrap" v-if="typeof weather.main != 'undefined' ">
        <div class="location-box">
          <div class="location">{{weather.name}}, {{weather.sys.country}}</div>
          <div class="date">{{dateBuilder()}}</div>
        </div> 
       

        <div class="weather-box">
          <div class="temp">{{Math.round(weather.main.temp)}}°F</div>
          <div class="weather">{{weather.weather[0].main}}</div>
          
        </div>
         
      </div>
    </main>
  </div> 
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      api_key: ,
      url_base: "http://api.openweathermap.org/data/2.5/",
      searching: '',
      weather: {},
      background: "container"
    }
  },
  methods:{
    fetchWeather(e) {
      if (e.key == "Enter") {
        fetch(`${this.url_base}weather?q=${this.searching}&units=imperial&appid=${this.api_key}`)
          .then(response => response.json())
          .then(this.setResults)
        
        
      }

      
    },
    setResults (results){
      this.weather = results;
      //Sets the class name for Background use later on
      if(this.weather != 'undefined'){
      this.background = this.weather.weather[0].main
      }
    },
    dateBuilder () {
      let d = new Date();
      let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
      let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];

      let day = days[d.getDay()]
      let date = d.getDate();
      let month = months[d.getMonth()]
      let year = d.getFullYear();

      return `${day} ${date} ${month} ${year}`;
    }
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body{
  font-family: 'montserrat', sans-serif;
}
#app {
  transition: 0.4s;
}

main{
  min-height: 100vh;
  padding: 25px;

}

.search-box{
  width: 90%;
  margin-bottom: 30px;
  z-index: 2;
}

.search-box .search-bar{
  display: block;
  width:100%;
  padding: 15px;

  color: #313131;
  font-size: 20px;

  appearance: none;
  border:none;
  outline:none;
  background: none;

  background-color: rgba(255,255,255,0.5);
  border-radius: 10px;
  transition: 0.4s;
}

.search-box .search-bar:focus{
  box-shadow: 0px 0px 16px rbga(0,0,0,0.25);
  background-color: rgba(255,255,255,0.75);
  border-radius: 17px;
}

.location-box .location {
  color: white;
  font-size:32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0,0,0,0.25);
}

.location-box .date{
  color:white;
  font-size:20px;
  font-weight: 300;
  font-style:italic;
  text-align: center;
}

.weather-box{
  text-align:center;
}

.weather-box .temp{
  display: inline-block;
  padding: 10px 25px;
  color: white;
  font-size: 102px;
  font-weight: 900;

  text-shadow: 3px 6px rgba(0,0,0,0.25);
  background-color: rgba(255,255,255,0.25);
  border-radius: 16px;
  margin: 30px 0px;

  box-shadow: 3px 6px rgba(0,0,0,0.25);
}

.weather-box .weather{
  color:white;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0,0,0,0.25);
}

.thunderstorm{

}

.drizzle{

}

.Rain{
  position:absolute;
  width: 100%;
  height: 100%;
  overflow: hidden;
  background: linear-gradient(to bottom, rgb(94, 140, 199),lightblue);

}

.Clear{
  position:absolute;
  width: 100%;
  height: 100%;
  overflow: hidden;
  background: linear-gradient(to bottom, rgb(63, 139, 238),lightblue);
}


.Clouds{
  position:absolute;
  width: 100%;
  height: 100%;
  overflow: hidden;
  background: linear-gradient(to bottom, rgb(161, 201, 253),lightblue)
}


.snow{
  position:absolute;
  width: 100%;
  height: 100%;
  overflow: hidden;
  background: linear-gradient(to bottom, rgb(143, 175, 218),lightblue)
}
.container{
  position:absolute;
  width: 100%;
  height: 100%;
  overflow: hidden;
  background: linear-gradient(to bottom, rgb(63, 139, 238),lightblue)
}

.elements div{
  position:absolute;
  width: 60px;
  height: 60px;
  background: rgba(255,255,255,0.5);
  border-radius: 50%;
}

.elements div:nth-child(1){
    top:11%;
    left:41%;
    animation: animate 10s linear infinite;
}

.elements div:nth-child(2){
    top:16%;
    left:49%;
    animation: animate 9s linear infinite;
}

.elements div:nth-child(3){
    top:32%;
    left:10%;
    animation: animate 9s linear infinite;
}

.elements div:nth-child(4){
    top:25%;
    left:78%;
    animation: animate 10s linear infinite;
}
.elements div:nth-child(5){
    top:20%;
    left:67%;
    animation: animate 10s linear infinite;
}
.elements div:nth-child(6){
    top:15%;
    left:80%;
    animation: animate 9s linear infinite;
}
.elements div:nth-child(7){
    top:2%;
    left:92%;
    height:80px;
    width:80px;
    background:rgb(255, 255, 39);
    animation: pulse 10s infinite; 
}

@keyframes animate{
    0%{
      transform: scale(0) translateX(-90px) rotate(360deg);
      opacity: 1;
    }
    100%{
      transform: scale(1) translateX(-90px) rotate(-180deg);
      border-radius:50%;
      opacity: 0;
    }
}
@keyframes pulse {
	0% {
		transform: scale(0.95);
		
	}
	70% {
		transform: scale(1.1);
	}

	100% {
		transform: scale(0.95);
	}
}


</style>
