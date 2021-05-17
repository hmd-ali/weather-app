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
        display: inline-block;
        padding: 1rem 1rem;
        background: #6E707A;
        color: #E7E7EB;
        border: none;
        border-radius: 1rem;
        font-size: 2rem;
;
    }
</style>