<template>
    <div class="container-main">
        <div class="container" v-if="defaultView">
            <img src="../assets/Cloud-background.png" alt="Cloud png" id="cloud">
            <div class="btn-container">
                <SearchButton @click="toggleSearch()" text="Search for places" class="bt1"/>
                <LocationButton class="bt2"/>
            </div>
            <div class="content">
                <div class="image-container">
                    <img  :src="require(`../assets/${returnSrc(data.weather_state_name)}.png`)" alt="state png">
                </div>
                <div class="weather-info">
                    <h1>{{Math.floor(data.the_temp)}}<span>&deg;C</span></h1>
                    <h2>{{data.weather_state_name}}</h2>
                </div>
            </div>
            <div class="footer">
                <p>Today &nbsp;&nbsp;&nbsp;&nbsp;.&nbsp;&nbsp;&nbsp;&nbsp; {{getDateString(data.applicable_date)}}</p>
                <p><i class="fas fa-map-marker-alt"></i>  {{location}}</p>
            </div>
        </div>
        <div class="search-container-main" v-if="!defaultView">
            <div class="search-container">
                <i @click="toggleSearch()" class="fas fa-times"></i>
                <div class="search bt1"><i class="fas fa-search"></i><input type="search" name="search" id="search" placeholder="Search Loaction" ></div>
                <button id="btn-search" @click="showLocations" class="bt2">Search</button>
            </div>

            <div class="location-container">
                <div class="location" :key="loc.value" v-for="loc in locations" @click="sendId(loc.woeid)">
                    <h1>{{loc.title}}</h1>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

import SearchButton from './SearchButton'
import LocationButton from './LocationButton'

export default {
    name: 'LeftPanel',
    components:{
        SearchButton,
        LocationButton,
    },
    props:{
        data: Object,
        location: String
    },
    emits:['send-id'],
    data(){
        return{
            StateName: this.data.weather_state_name,
            date :this.data.applicable_date,
            temp: Math.floor(this.data.the_temp),
            defaultView: true,
            locations: [],
            query : '',
        }
    },
    methods:{
        sendId(id){
            this.$emit('send-id' , id)
            this.locations = []
            this.defaultView = !this.defaultView
        },
        toggleSearch(){
            this.defaultView = !this.defaultView
        },
        returnSrc(weatherState){
            const states = {
                'Snow' : 'Snow',
                'Sleet' : 'Sleet',
                'Hail' : 'Hail',
                'Thunderstorm' : 'Thunderstorm',
                'Heavy Rain' : 'HeavyRain',
                'Light Rain' : 'LightRain',
                'Showers' : 'Shower',
                'Heavy Cloud' : 'HeavyCloud',
                'Light Cloud' : 'LightCloud',
                'Clear' : 'Clear'
            }
            const state = states[weatherState]
            return state
        },
        getDateString(mydate) {
            const date = new Date(mydate)
            const months = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Now', 'Dec']
            const days = ['Mon.', 'Tue.','Wed.', 'Thu.', 'Fri.', 'Sat.', 'Sun.']
            let day = days[date.getDay()]
            let weekDay = date.getDate()
            let month = months[date.getMonth()]

            return day + " " + weekDay + " " + month
        },
        async fetchLoaction(query){
            const apiFetchUrl = 'https://api.allorigins.win/raw?url='
            const apiUrl = 'https://www.metaweather.com/api/location/'
            let url = `${apiFetchUrl}${apiUrl}search/?query=`+query
            let res = await fetch(`${url}`)
            let data = await res.json()
            return data
        },
        async showLocations(){
            this.locations = []
            this.query = document.getElementById('search').value
            this.locations = await this.fetchLoaction(this.query)
        },
    },
    async created(){
        this.query = document.getElementById('search').value
        this.StateName = await this.data.weather_state_name
        this.date = await this.data.applicable_date
    }
}    
</script>

<style scoped>
    .container-main{
        position: relative;
        height: 100%;
        width: 33%;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: space-between;
        background: #1E213A;
        overflow: hidden;
        padding: 4rem 0 2rem 0;
    }
    .container{
        display: flex;
        width: 100%;
        height: 100%;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: space-between;

    }
    #cloud{
        position: absolute;
        top: 103px;
        left: -40px;
        width: 130%;
        opacity: 0.1;
    }
    .btn-container{
        position: relative;
        width: 100%;
        /* padding: 4rem 6rem; */
        /* padding: 8% 8%; */
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
    .content{
        position: relative;
        width: 100%;
        display: flex;
        flex-direction: column;
        align-items: center;
        padding: 0 4rem;
    }

    .content .image-container img{
        width: 90%;
        object-fit: cover;
    }
    .content .weather-info{
        color: #E7E7EB;
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    .content .weather-info h1{
        font-size: 14.4rem;
        font-weight: 500;
    }
    .content .weather-info h1 span{
        font-size: 4.8rem;
        font-weight: 500;
        opacity: 0.5;
    }
    .content .weather-info h2{
        color: #A09FB1;
        font-weight: 600;
        font-size: 3.6rem;
    }
    .footer{
        text-align: center;
        color: #88869D;
    }
    .footer p{
        font-size: 2rem;
        margin-top: 2rem;
    }
    .footer p:first-child{
        font-size: 1.8rem;
        font-weight: 500;
    }
    .footer p:last-child{
        font-size: 1.8rem;
        font-weight: 600;
    }
    .bt1{
        margin-left: 5rem;
    }
    .bt2{
        margin-right: 5rem;
    }
    .search-container-main{
        position: relative;
        height: 100%;
        width: 100%;
        display: flex;
        flex-direction: column;
    }
    .search-container{
        width: 100%;
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 1rem 2rem;
    }

    .search-container #btn-search{
        background: #3C47E9;
        border: none;
        padding: 1.5rem 2rem;
        color: #E7E7EB;
        font-size: 1.6rem;
    }
    .search-container #btn-search:hover{
        cursor: pointer;
        background: #2a33b1;
    }
    .search-container .search{
        width: 50%;
        height: 48px;
        position: relative;
    }
    .search-container #search{
        width: 100%;
        border: none;
        height: 100%;
        outline: #E7E7EB 1px solid;
        background: transparent;
        padding: .5rem 0 .5rem 5rem;
        color: #E7E7EB;
        font-size: 1.6rem;

    }
    .fa-search{
        position: absolute;
        left:5%;
        bottom: 50%;
        font-size: 1.6rem;
        color: #E7E7EB;
        transform: translateY(50%);
    }

    .location-container{
        position: relative;
        padding: 1rem 2rem;
        width: 100%;
        color: #616475;
        overflow-y: auto;
    }

    .location-container .location{
        position: relative;
        margin: 0 5rem 0 5rem;
        padding: 2rem 2rem;
    }

    .location-container .location::after{
        content: '';
        position: absolute;
        right: 5%;
        bottom: 50%;
        transform: translateY(-50%);
        border: solid #E7E7EB;
        border-width: 0 3px 3px 0;
        display: inline-block;
        padding: 3px;
        transform: rotate(-45deg);
        -webkit-transform: rotate(-45deg);

    }

    .location-container .location:hover{
        cursor: pointer;
        border: #616475 1px solid;
        color: #E7E7EB;
    }
    .location-container .location:hover::after{
        content: '';
        position: absolute;
        bottom: 50%;
        /* transform: translateY(-50%); */
        border: solid #E7E7EB;
        border-width: 0 4px 4px 0;
        display: inline-block;
        padding: 3px;
        transform: rotate(-45deg) translateX(10px) scale(1.2);
        -webkit-transform: rotate(-45deg) translateX(10px) scale(1.2);
    }
    .fa-times{
        position: absolute;
        right: 2%;
        top: -2%;
        font-size: 2.5rem;
        color:#A09FB1;
    }
    .fa-times:hover{
        cursor: pointer;
        color: #E7E7EB;
    }
    
</style>