<template>
    <div class="card">
        <div class="card-header">
            <h1>{{ title }}</h1>
        </div>
        <div class="card-body">
            <slot></slot>
        </div>
    </div>
</template>

<script>

export default {
    name: "VCard",
    props: ['title'],
}

</script>