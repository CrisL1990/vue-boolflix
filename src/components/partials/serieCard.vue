<template>
    <div>
        <ul>
            <div class="img-cont position-relative">
                <div class="flip-card-inner">

                    <!--Inizio poster film-->
                    <div class="front">
                        <li v-if="serieCard.poster_path"><img :src="imgUrl" alt=""></li>
                        <li v-else><img class="img-fluid" src="../../assets/img/movie-clapboard.jpeg" alt=""></li>
                    </div>
                    <!--Fine poster film-->

                    <!--Inizio Info film-->
                    <div class="back">
                        <div class="info-box position-absolute">

                            <!--Inizio titolo-->
                            <li><span>Titolo: </span>{{serieCard.name}}</li>
                            <li><span>Titolo originale: </span>{{serieCard.original_name}}</li>
                            <li v-if="serieCard.original_language != ''"><span>Lingua: </span><LangFlag :iso="serieCard.original_language"/>{{' ' + serieCard.original_language}}</li>
                            <!--Fine titolo-->

                            <!--Inizio voto-->
                            <li>
                                <span>Voto: </span>
                                <span v-for="(number, i) in 5" :key="i">
                                    <i :class="(number <= vote) ? 'fa-solid fa-star yellow' : 'fa-regular fa-star'"></i>
                                </span>
                            </li>
                            <!--Fine voto-->

                            <!--Inizio overview-->
                            <li v-if="serieCard.overview"><span>Overview: </span>{{serieCard.overview}}</li>
                            <li v-else>Descrizione non disponibile</li>
                            <!--Fine overview-->

                            <!--Inizio cast-->
                            <div>Actors:</div>
                            <li><span updateCast></span><span v-for="(actor, index) in 5" :key="index">{{cast[index].name}}, </span></li>
                            <!--Fine cast-->

                            <!--Inizio generi-->
                            <div>Genre:</div>
                            <li>
                                <span v-for="(genre, index) in serieCard.genre_ids" :key="index">
                                    <span v-for="(item, i) in genres" :key="i">
                                        <span v-if="(genre == item.id)">{{item.name}}, </span>     
                                    </span>
                                </span>
                            </li>
                            <!--Fine generi-->
                        </div>
                    </div>
                    <!--Fine info film-->
                </div>
            </div>
        </ul>
    </div>
</template>

<script>
import LangFlag from 'vue-lang-code-flags';

const axios = require('axios');

export default {
    name: 'serieCard',

    data(){
        return{
            toggle: false,
            imgUrl: 'https://image.tmdb.org/t/p/' + 'w342' + this.serieCard.poster_path,
            vote: Math.ceil(this.serieCard.vote_average / 2),
            id: this.serieCard.id,
            cast: [],
            genres: [],    
        }
    },

    props:{
        'serieCard': Object,
    },

    components:{
        LangFlag,
    },

    methods:{

        //Esegue chiamata API per membri del cast
        callCastApi: function(filmId){
            axios.get('https://api.themoviedb.org/3/tv/' + filmId +'/credits?api_key=918e2ad402623b3f2672adefc7b3a96f&language=en-US') 

            .then((response) => {  
                this.cast = response.data.cast;
            })
            .catch(function (error) {
                // handle error
                console.log(error);
            })
            
            return this.cast
        },

        //Esegue chiamata API per lista generi
        callGenres: function(){
            axios.get('https://api.themoviedb.org/3/genre/tv/list?api_key=918e2ad402623b3f2672adefc7b3a96f&language=en-US')

            .then((response) => {  
                this.genres = response.data.genres;
            })

            .catch(function (error) {
                // handle error
                console.log(error);
            })
            return this.genres
        }
    },

    //Richiama le due funzioni per la chiamata API al mounted
    mounted(){
        this.callCastApi(this.id)
        this.callGenres()
    },

}
</script>

<style scoped lang="scss">
    //Importa stilizzazione grafica della singola card
    @import "../../assets/scss/cards.scss";
</style>


