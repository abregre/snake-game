<template>
    <h2>Ranking List</h2>
    <ul class="rankings">
        <li v-for="(rank,i) in rankingsList" :key="i">{{rank.username}} : {{rank.score}}</li>
    </ul>
</template>

<script>
    export default {
        props: {
            rankingsList: Array
        }
    }
</script>

<style scoped>
.rankings{
    list-style: none;
    padding: 0;
}
</style>