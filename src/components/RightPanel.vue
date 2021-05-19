<template>
<div class="container">
    <!-- <p>{{data.consolidated_weather[0].humidity}}</p> -->
    <div class="temp-button-container">
        <TempButton text="&deg;C" :tempStatus="tempStatus"/>
        <TempButton text="&deg;F" :tempStatus="!tempStatus"/>
    </div>
    <div class="weather-data">
        <WeatherDay :data="data.consolidated_weather[1]" day='Tomorrow'/>
        <WeatherDay :data="data.consolidated_weather[2]" :day='getDateString(data.consolidated_weather[2].applicable_date)'/>
        <WeatherDay :data="data.consolidated_weather[3]" :day='getDateString(data.consolidated_weather[3].applicable_date)'/>
        <WeatherDay :data="data.consolidated_weather[4]" :day='getDateString(data.consolidated_weather[4].applicable_date)'/>
        <WeatherDay :data="data.consolidated_weather[5]" :day='getDateString(data.consolidated_weather[5].applicable_date)'/>
    </div>
    <div class="highlights-container">
        <h1>Today's highlights</h1>
        <div class="wind-humidity">
            <Wind :data='data.consolidated_weather[0]'/>
            <Humidity :data='data.consolidated_weather[0]'/>
        </div>
        <div class="detail-container">
            <VisPress text='Visibility' units='miles' :data='data.consolidated_weather[0].visibility'/>
            <VisPress text='Air Pressure' units='mb' :data='data.consolidated_weather[0].air_pressure'/>
        </div>
    </div>
    <footer><p>created by <span>Cake</span></p></footer>
</div>
</template>

<script>

import WeatherDay from './WeatherDay'
import TempButton from './TempButton'
import VisPress from './VisPress'
import Wind from './Wind'
import Humidity from './Humidity'

export default {
    name: 'RightPanel',
    components:{
        TempButton,
        WeatherDay,
        VisPress,
        Wind,
        Humidity
    },
    props:{
        data: Object,
        tempStatus: Boolean,
    },
    methods:{
        getDateString(mydate) {
            const date = new Date(mydate)
            const months = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Now', 'Dec']
            const days = ['Mon.', 'Tue.','Wed.', 'Thu.', 'Fri.', 'Sat.', 'Sun.']
            let day = days[date.getDay()]
            let weekDay = date.getDate()
            let month = months[date.getMonth()]

            return day + " " + weekDay + " " + month
        }
    },

    

}
</script>

<style scoped>
    .container{
        position: relative;
        width: 67%;
        height: 100vh;
        display: flex;
        flex-direction: column;
        align-items: center;
        /* justify-content: space-around; */
        background: #100E1D;
    }
    .temp-button-container{
        position: relative;
        width: 100%;
        padding: 2rem 2rem;
        display: flex;
        justify-content: flex-end;
    }

    .weather-data{
        position: relative;
        width: 100%;
        max-width: 1000px;
        padding: 1rem 10rem;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    .highlights-container{
        position: relative;
        width: 100%;
        max-width: 1000px;
        padding: 1rem 10rem;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        align-items: center;
        color: #E7E7EB;
    }

    .highlights-container h1{
        width: 100%;
    }
    .highlights-container .wind-humidity{
        position: relative;
        width: 100%;
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-top: 3rem;

    }
    .highlights-container .detail-container{
        position: relative;
        width: 100%;
        display: flex;
        align-items: center;
        justify-content: space-between;
        margin-top: 3rem;
    }
    footer{
        position: absolute;
        bottom: 0;
        width: 100%;
        color: #A09FB1;
        font-size: 1.4rem;
        text-align: center;
        padding: 2rem 2rem;

    }

    footer span{
        font-weight: 700;
    }

</style>