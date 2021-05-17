<template>
    <div class="container3">
        <h2>Humidity</h2>
        <div class="data">
            <p>{{value}}</p>
            <p>%</p>
        </div>
        <div class="bar">
            <div class="values">
                <span>0</span>
                <span>50</span>
                <span>100</span>
            </div>
            <div class="unit">%</div>
            <div class="progress" :style="{width: value +'%'}"></div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Humidity',
    props:{
        data: Array,
    },
    data(){
        return{
            value: Math.floor(this.data.humidity),
        }
    }
}
</script>

<style scoped>
    .container3{
        position: relative;
        width: 328px;
        height: 204px;
        display: flex;
        flex-direction: column;
        justify-content: space-evenly;
        align-items: center;
        background: #1E213A;
        color: #E7E7EB;
    }
    .container3 h2{
        font-size: 1.6rem;
        font-weight: 500;
    }
    .container3 .data{
        display: flex;
        align-items: center;
        line-height: 70px;
    }

    .container3 .data p:first-child{
        font-size: 6.4rem;
        font-weight: 700;
        margin-right: .5rem;
    }

    .container3 .data p:last-child{
        font-size: 3.2rem;
        font-weight: 400;
        transform: translateY(1rem);
        margin-left: .5rem;

    }

    .bar{
        position: relative;
        width: 70%;
        height: 8px;
        background: #E7E7EB;
        border-radius: 8rem;
        font-size: 1.4rem;
        font-weight: 700;
    }

    .bar .values{
        position: absolute;
        left: 0;
        top: -17px;
        width: 100%;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    .bar .unit{
        position: absolute;
        left: 0;
        bottom: -17px;
        width: 100%;
        display: flex;
        justify-content: flex-end;
        align-items: center;
    }
    .bar .progress{
        height: 100%;
        background: #FFEC65;
        border-radius: 8rem;
    }
</style>