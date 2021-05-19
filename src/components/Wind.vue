<template>
    <div class="container2">
        <h2>Wind Status</h2>
        <div class="data">
            <p class="value">{{Math.floor(data.wind_speed)}}</p>
            <p class="unit">mph</p>
        </div>
        <div class="direction">
            <!-- <i class="fas fa-location-arrow" :style="style"></i> -->
            <i class="fas fa-location-arrow" :style="{ transform: 'rotate(' + (Math.floor(data.wind_direction)-45) + 'deg)'}"></i>
            <p>{{data.wind_direction_compass}}</p>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Wind',
    props:{
        data:Object
    },
}
</script>

<style scoped>
    .container2{
        position: relative;
        width: 328px;
        height: 204px;
        background: #1E213A;
        display: flex;
        flex-direction: column;
        justify-content: space-evenly;
        align-items: center;
    }
    .container2 h2{
        font-size: 1.6rem;
        font-weight: 500;
    }
    .container2 .data{
        display: flex;
        justify-content: space-between;
        align-items: center;
        font-weight: 700;
    }
    .container2 .data p:first-child{
        margin-right: .5rem;
        font-size: 6.4rem;
    }
    .container2 .data p:last-child{
        margin-left: .5rem;
        font-size: 3.2rem;
        transform: translateY(1rem);
    }
    .container2 .direction{
        display: flex;
        justify-content: space-between;
        align-items: center;
        font-weight: 500;
    }
    .container2 .direction i{
        background: rgba(255, 255, 255, 0.3);
        border-radius: 50%;
        padding: 1rem 1rem;
        font-size: 1.5rem;
        margin-right: .5rem;
        /* transform: rotate(-45deg); */
    }
    .container2 .direction p{
        margin-left: .5rem;
        font-size: 1.4rem;
    }
</style>