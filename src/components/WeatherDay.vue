<template>
    <div class="day-container">
        <p class="day">{{day}}</p>
        <div class="img-container">
            <img  :src="require(`../assets/${returnSrc(StateName)}.png`)" alt="state png">
        </div>
        <div class="min-max">
            <p>{{minTemp}}&deg;C</p>
            <p>{{maxTemp}}&deg;C</p>
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
            image:{
                Snow:require('../assets/Snow.png'),
                Sleet:require('../assets/HeavyRain.png'),
                Hail:require('../assets/Hail.png'),
                Thunderstorm:require('../assets/Thunderstorm.png'),
                HeavyRain:require('../assets/HeavyRain.png'),
                LightRain:require('../assets/LightRain.png'),
                Showers:require('../assets/Shower.png'),
                HeavyCloud:require('../assets/HeavyCloud.png'),
                LightCloud:require('../assets/LightCloud.png'),
                Clear:require('../assets/Clear.png'),
            },

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
            console.log(states['Hail'])
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
        color: white;
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
        font-size: 1.5rem;
    }

    .day{
        font-size: 1.2rem;
    }
    
</style>