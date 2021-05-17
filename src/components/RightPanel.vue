<template>
<div class="container">
    <!-- <p>{{data.consolidated_weather[0].humidity}}</p> -->
    <div class="temp-button-container">
        <TempButton text="&deg;C" :tempStatus="tempStatus"/>
        <TempButton text="&deg;F" :tempStatus="!tempStatus"/>
    </div>
    <div class="weather-data">
        <WeatherDay :data="data.consolidated_weather[1]" day='Tomorrow'/>
        <WeatherDay :data="data.consolidated_weather[2]" :day='data.consolidated_weather[1].applicable_date'/>
        <WeatherDay :data="data.consolidated_weather[3]" :day='data.consolidated_weather[2].applicable_date'/>
        <WeatherDay :data="data.consolidated_weather[4]" :day='data.consolidated_weather[3].applicable_date'/>
        <WeatherDay :data="data.consolidated_weather[5]" :day='data.consolidated_weather[4].applicable_date'/>
    </div>
    <div class="highlights-container">
        <h1>Today's highlights</h1>
        <div class="container">
            <VisPress text='Visibility' units='miles' :data='data.consolidated_weather[0].visibility'/>
            <VisPress text='Air Pressure' units='mb' :data='data.consolidated_weather[0].air_pressure'/>
        </div>
    </div>
</div>
</template>

<script>

import WeatherDay from './WeatherDay'
import TempButton from './TempButton'
import VisPress from './VisPress'

export default {
    name: 'RightPanel',
    components:{
        TempButton,
        WeatherDay,
        VisPress,
    },
    props:{
        data: Object,
        tempStatus: Boolean,
    }


}
</script>

<style scoped>
    .container{
        position: relative;
        width: 67%;
        height: 100vh;
        display: flex;
        flex-direction: column;
        /* align-items: center; */
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
        padding: 1rem 10rem;
        display: flex;
        justify-content: space-evenly;
    }

    .highlights-container{
        width: 100%;
        padding: 2rem 2rem;
        display: flex;
        flex-direction: column;
        color: #E7E7EB;
    }

</style>