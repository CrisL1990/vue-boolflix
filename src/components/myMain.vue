<template>
<!-- Crea la card del film-->
    <main>
        

        <div v-if="movieCards.length > 0">
            <h1>FILM</h1>
            <filmCard v-for="(movie, index) in movieCards" :key="index" :movieCard="movie"/>
        </div>

        <div v-if="serieCards.length > 0">
            <h1>SERIE</h1>
            <serieCard v-for="(serie, index) in serieCards" :key="index" :serieCard="serie"/>
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
        'searching': Boolean
    }
}
</script>

<style scoped lang="scss">

</style>