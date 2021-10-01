<template>
        <div v-if="!isLoaded" class="pre-loader">
            <h1>Loading...</h1>
            <div class="squares">
                <div class="square left"></div>
                <div class="square"></div>
                <div class="square"></div>
                <div class="square"></div>
                <div class="square right"></div>
            </div>
        </div>
</template>

<script>
    export default {
        name: 'PreLoader',
        data(){
            return{
                isLoaded: false
            }
        },
        mounted(){
            document.body.classList.add('no-scroll')
            document.onreadystatechange = () => {
                if( document.readyState == 'complete'){
                    document.body.classList.remove('no-scroll')
                    this.isLoaded = true // Code to hide pre-loader
                    console.log('complete')
                }
            }
        }
    }
</script>

<style scoped>
    .pre-loader{
        position: fixed;
        background: #100e1d;
        z-index: 9999;
        width: 100%;
        height: 100vh;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }
    .pre-loader h1{
        font-size: 3rem;
        color: white;
    }
    .pre-loader .squares{
        width: 100%;
        position: relative;
        display: flex;
        justify-content: center;
        align-items: center;
        margin: 2rem;
    }
    .pre-loader .squares .square{
        width: 2rem;
        height: 2rem;
        background: white;
        margin: 1rem;
    }
    .left{
        animation: left 1s infinite;
    }
    .right{
        animation: right 1s infinite;
        animation-delay: .5s;
    }
    @keyframes left {
        40%{
            transform: translateX(-1rem);
        }
        50%{
            transform: translateX(0);
        }
    }
    @keyframes right {
        40%{
            transform: translateX(1rem);
        }
        50%{
            transform: translateX(0);
        }
    }
</style>