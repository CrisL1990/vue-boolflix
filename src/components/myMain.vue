<template>
<!-- Crea la card del film-->
    <main class="container">
        
        <h1 v-if="movieCards.length > 0" class="mx-4 my-5">FILM</h1>

        <div class="d-flex flex-wrap row-cols-lg-3" v-if="movieCards.length > 0">
            <filmCard class="col" v-for="(movie, index) in movieCards" :key="index" :movVotes="movVotes" :movieCard="movie"/>
        </div>

        <h1 v-if="movieCards.length > 0" class="mx-4 my-5">SERIE</h1>

        <div class="d-flex flex-wrap row-cols-lg-3" v-if="serieCards.length > 0">
            <serieCard class="col" v-for="(serie, index) in serieCards" :key="index" :serVotes="serVotes" :serieCard="serie"/>
        </div>
        
        
    </main>
</template>

<script>
import filmCard from './partials/filmCard.vue'
import serieCard from './partials/serieCard.vue'


export default {
    name: 'myMain',

    components:{
        filmCard,
        serieCard
    },

    data(){
        return{


        }

    },

    props:{
        'movieCards': Array,
        'serieCards': Array,
        'movVotes': Array,
        'serVotes': Array,
        'searching': Boolean
    },

}
</script>

<style scoped lang="scss">
    @import "../assets/scss/common.scss";

    h1{
        color: white;
    }
</style>