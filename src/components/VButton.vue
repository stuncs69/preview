<template>
    <div>
        {{ this.text }}
    </div>
</template>

<style scoped>

div {
    width: fit-content;
    height: min-content;
    padding: 1rem;
    background-color: red;
    color: white;
    transition: 300ms;
    cursor: pointer;
    font-size: x-large;
    border-radius: 0.4rem;
}

div:hover {
    background-color: maroon;
}

</style>

<script lang="ts">

export default {
    props: {
        text: String
    }
}

</script>