<template>
    <button class="btn btn-primary">
        {{ this.text }}
    </button>
</template>

<script lang="ts">

export default {
    props: {
        text: String
    }
}

</script>