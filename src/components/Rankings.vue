<template>
    <h2>Ranking List</h2>
    <ul class="rankings">
        <li>{{username}} : {{score}}</li>
    </ul>
</template>

<script>
    export default {
        props: {
            username: String,
            score: Number
        }
    }
</script>

<style scoped>

</style>