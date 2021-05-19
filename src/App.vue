<template>
  <div class="wrapper">
    <LeftPanel @send-id="sendId" :data="weather.consolidated_weather[0]" :location="weather.title"/>
    <RightPanel :data="weather" :tempStatus="tempActive"/>
  </div>
  
</template>

<script>

import  LeftPanel  from './components/LeftPanel'
import RightPanel from './components/RightPanel'


export default {
  name: "App",
  components: {
    LeftPanel,
    RightPanel
  },
  data(){
    return{
      weather:[],
      tempActive: true,
      locID : 2487956,
    }
  },
  methods:{
    async sendId(id){
      this.locID = await id
      console.log('loc' ,this.locID)
      this.weather = await this.fetchWeather(id)

    },
    async fetchWeather(id){
      const apiFetchUrl = 'https://api.allorigins.win/raw?url='
      const apiUrl = 'https://www.metaweather.com/api/location/'
      // let location = await this.fetchLocation()
      let url = `${apiFetchUrl}${apiUrl}${id}`
      let res = await fetch(`${url}`)
      let data =  await res.json()
      // console.log("hi")
      // console.log(data)
      console.log(url)
      return data
    }
    
    
  },
  async created(){
      this.weather = await this.fetchWeather(this.locID)
      // this.locID = await this.sendId(id)
    },

  
};


</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Raleway:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap');

  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  html{
    font-size: 62.5%;
    font-family: "Raleway",sans-serif;
  }

  .wrapper{
    width: 100%;
    height: 100vh;
    position: relative;
    display: flex;
  }



</style>
