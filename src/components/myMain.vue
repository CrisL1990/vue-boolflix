<template>
    <main>
        <div v-if="movieCards.length > 0">
            <ul v-for="(movie, index) in movieCards" :key="index">
                <li>{{movie.title}}</li>
                <li>{{movie.original_title}}</li>
                <li>{{movie.original_language}}</li>
                <li>{{movie.vote_average}}</li>
            </ul>
        </div>
        <div v-if="movieCards.length == 0 && searching">NON CI SONO RISULTATI</div>
    </main>
</template>

<script>
export default {
    name: 'myMain',

    data(){
        return{
            
        }

    },

    props:{
        'movieCards': Array,
        'searching': Boolean
    }
}
</script>

<style scoped lang="scss">

</style>