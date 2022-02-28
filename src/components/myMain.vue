<template>
<!-- Crea la card del film-->
    <main>
        <div v-if="movieCards.length > 0">

            <filmCard v-for="(movie, index) in movieCards" :key="index" :movieCard="movie"/>
            <!--
            <ul v-for="(movie, index) in movieCards" :key="index">
                <li>{{movie.title}}</li>
                <li>{{movie.original_title}}</li>
                <li>{{movie.original_language}}</li>
                <li>{{movie.vote_average}}</li>
            </ul>
            -->
        </div>
    </main>
</template>

<script>
import filmCard from './partials/filmCard.vue'

export default {
    name: 'myMain',

    components:{
        filmCard
    },

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