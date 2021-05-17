<template>
    <div class="air-container">
        <h1>{{text}}</h1>
        <p class="text-data"><span>{{Data}}</span> {{units}}</p>
    </div>
</template>

<script>
export default {
    name: 'VisPress',
    props:{
        text: String,
        units: String,
        data: Number
    },
    data(){
        return{
            Data:Math.floor(this.data)
            
        }
    }

}
</script>

<style scoped>
    .air-container{
        position: relative;
        width: 328px;
        height: 160px;
        display: flex;
        flex-direction: column;
        justify-content: space-around;
        align-items: center;
        background: #1E213A;
        color: #E7E7EB;
    }
    h1{
        font-size: 1.5rem;
        font-weight: 300;
    }
    .text-data{
        font-size: 3rem;
    }
    .text-data span{
        font-size: 5rem;
        font-weight: 700;
    }

</style>