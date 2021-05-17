<template>
    <div class="container">
        <div class="bg-cloud">
            <img src="../assets/Cloud-background.png" alt="Cloud png" id="cloud">
        </div>
        <div class="btn-container">
            <SearchButton  text="Search for places" class="bt1"/>
            <LocationButton class="bt2"/>
        </div>
        <div class="content">
            <div class="image-container">
                <img  :src="require(`../assets/${returnSrc(StateName)}.png`)" alt="state png">
            </div>
            <h1>15 &deg;C</h1>
            <h2>{{StateName}}</h2>
        </div>
        <div class="footer">
            <p>Today &nbsp;&nbsp;&nbsp;&nbsp;.&nbsp;&nbsp;&nbsp;&nbsp; {{getDateString(date)}}</p>
            <p>{{location}}</p>
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
    data(){
        return{
            StateName: this.data.weather_state_name,
            date :this.data.applicable_date,
            
        }
    },
    methods:{
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
    }
}    
</script>

<style scoped>
    .container{
        position: relative;
        height: 100vh;
        width: 33%;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: space-between;
        background: #1E213A;
        overflow: hidden;
        padding: 2rem 0;
    }

    .bg-cloud{
        
        width: 100%;
    }

    .bg-cloud #cloud{
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
        /* height: 230px; */
        object-fit: cover;
    }
    .content h1,.content h2{
        margin-top: 4rem;
        color: #E7E7EB;
        font-size: 7rem;
        font-weight: 400;
    }
    .footer{
        text-align: center;
    }
    .footer p{
        color: #E7E7EB;
        font-size: 2rem;
        margin-top: 2rem;
    }
    .bt1{
        margin-left: 5rem;
    }
    .bt2{
        margin-right: 5rem;
    }
</style>