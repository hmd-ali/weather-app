<template>
    <div class="container">
        <div class="bg-cloud">
                <img src="../assets/Cloud-background.png" alt="Cloud png" id="cloud">
        </div>
        <div class="top">

        </div>
    </div>
</template>

<script>
export default {
    name: 'LeftPanel',
}
</script>

<style scoped>
    .container{
        position: relative;
        height: 100vh;
        width: 33%;
        display: flex;
        flex-direction: column;
        justify-content: space-around;
        align-items: center;
        background: #1E213A;
        overflow: hidden;
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
</style>