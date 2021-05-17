<template>
  <div class="wrapper">
    <LeftPanel />
    <RightPanel :data="this.weather" :tempStatus="this.tempActive"/>
    <!-- <p style="color:white;background:red;width:100px;">{{weather}}</p> -->
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
    }
  },
  methods:{
    async fetchLocation(){
      const apiFetchUrl = 'https://api.allorigins.win/raw?url='
      const apiUrl = 'https://www.metaweather.com/api/location/'
      let url = `${apiFetchUrl}${apiUrl}search/?query=san`
      const res = await fetch(`${url}`)
      const data = await res.json()
      // console.log(data[0].woeid)
      return data[0].woeid
    },
    async fetchWeather(){
      const apiFetchUrl = 'https://api.allorigins.win/raw?url='
      const apiUrl = 'https://www.metaweather.com/api/location/'
      // let location = await this.fetchLocation()
      let location = 1105779
      let url = `${apiFetchUrl}${apiUrl}${location}`
      const res = await fetch(`${url}`)
      const data =  await res.json()
      // console.log("hi")
      // console.log(data)
      return data
    }
    
    
  },
  async created(){
      this.weather = await this.fetchWeather()
    },

  
};


</script>

<style>
  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  html{
    font-size: 62.5%;
    font-family: "Poppins",sans-serif;
  }

  .wrapper{
    width: 100%;
    height: 100vh;
    position: relative;
    display: flex;
  }



</style>
