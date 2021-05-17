<template>
    <div class="day-container">
        <p class="day">{{day}}</p>
        <div class="img-container">
            <img  :src="require(`../assets/${returnSrc(StateName)}.png`)" alt="state png">
        </div>
        <div class="min-max">
            <p>{{maxTemp}}&deg;C</p>
            <p>{{minTemp}}&deg;C</p>
        </div>
    </div>
</template>

<script>
export default {
    name: 'WeatherDay',
    props:{
        data:Object,
        day: String
    },
    data(){
        return{
            minTemp:Math.floor(this.data.min_temp),
            maxTemp:Math.floor(this.data.max_temp),
            StateName: this.data.weather_state_name,


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
        }
    },

}
</script>

<style scoped>
    .day-container{
        position: relative;
        width: 120px;
        height: 177px;
        display: flex;
        flex-direction: column;
        justify-content: space-evenly;
        align-items: center;
        background: #1E213A;
        color: #E7E7EB;
    }
    .day-container p:first-child{
        font-size: 1.6rem;
        font-weight: 500;
    }
    .img-container{
        position: relative;
        width: 100%;
        height: 50px;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .img-container img{
        width: 60%;
    }
    /* img{
        width: 70%;
    } */
    .min-max{
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    .min-max p{
        display: inline-block;
        margin: 1rem;
        font-size: 1.6rem;
    }
    .min-max p:last-child{
        color: #A09FB1;
    }

    .day{
        font-size: 1.2rem;
    }
    
</style>