<template>
    <button>
        {{ this.text }}
    </button>
</template>

<style scoped>

button {
    width: fit-content;
    height: min-content;
    padding: 1rem;
    background-color: red;
    color: white;
    transition: 300ms;
    cursor: pointer;
    font-size: x-large;
    border-radius: 0.4rem;
    border: none;
}

button:hover {
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