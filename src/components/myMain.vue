<template>
<!-- Crea la card del film-->
    <main class="container">
        
        <h1 v-if="movieCards.length > 0" class="mx-4 my-5">FILM</h1>
        
        <div class="d-flex flex-wrap row-cols-lg-3" v-if="movieCards.length > 0">
            <filmCard class="col" v-for="(movie, index) in movieCards" :key="index" :movVotes="movVotes" :movieCard="movie" :genere="genere"/>
        </div>

        <h1 v-if="movieCards.length > 0" class="mx-4 my-5">SERIE</h1>

        <div class="d-flex flex-wrap row-cols-lg-3" v-if="serieCards.length > 0">
            <serieCard class="col" v-for="(serie, index) in serieCards" :key="index" :serVotes="serVotes" :serieCard="serie"/>
        </div>
        
        
    </main>
</template>

<script>

//const axios = require('axios');

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
            //generi: [],
            toggle: false,
        }

    },

    props:{
        'movieCards': Array,
        'serieCards': Array,
        'movVotes': Array,
        'serVotes': Array,
        'searching': Boolean,

        'genere': String
    },

    methods:{

        /*
        callGenres: function(){
            axios.get('https://api.themoviedb.org/3/genre/movie/list?api_key=918e2ad402623b3f2672adefc7b3a96f&language=en-US')

            .then((response) => {  
                this.generi = response.data.genres;
            })
            
            .catch(function (error) {
                // handle error
                console.log(error);
            })
            return this.generi
        },
        */
    },

    mounted(){
        //this.callGenres()
    },

    
}


</script>

<style scoped lang="scss">
    @import "../assets/scss/common.scss";

    h1{
        color: white;
    }
</style>