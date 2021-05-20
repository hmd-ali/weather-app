<template>
    <button>{{text}}</button>
</template>

<script>
export default {
    name: 'SearchButton',
    props: {
        text: String,
    }
}
</script>

<style scoped>
    button{
        padding: 1rem 1rem;
        background: #6E707A;
        color: #E7E7EB;
        border: none;
        border-radius: 1rem;
        font-size: 2rem;
    }
    button:hover{
        background: #E7E7EB;
        color: #111111;
        cursor: pointer;
    }
</style>