<template>
    <button v-bind:class="[tempStatus ? 'active' : '' ]" @click="$emit(onClick())">{{text}}</button>
</template>

<script>
export default {
    name: 'TempButton',
    props: {
        text: String,
        tempStatus:Boolean,
    },
    methods:{
        onClick(){
            this.emit('temp-btn-click',this.tempStatus)
        }
    }
}
</script>

<style scoped>
    button{
        background:#585676;
        color: #E7E7EB;
        font-size: 1.6rem;
        font-weight: 500;
        border-radius: 50%;
        width: 30px;
        height: 30px;
        border: none;
        padding: .5rem;
        margin: 1rem;
    }
    button.active{
        background: #E7E7EB;
        color: #110E3C;
    }
</style>