<template>
    
    <div>
        <ul :class="(miaFunzione == true || genere == '') ? '' : 'd-none' ">
            <div class="img-cont position-relative">
                <div class="flip-card-inner">

                    <!--Inizio poster film-->
                    <div class="front">
                        <li v-if="movieCard.poster_path"><img :src="imgUrl" alt=""></li>
                        <li v-else><img class="img-fluid" src="../../assets/img/movie-clapboard.jpeg" alt=""></li>
                    </div>
                    <!--Fine poster film-->

                    <!--Inizio Info film-->
                    <div class="back">
                        <div class="info-box position-absolute">
                                
                            <!--Inizio titolo-->
                            <li><span>Titolo: </span>{{movieCard.title}}</li>
                            <li><span>Titolo originale: </span>{{movieCard.original_title}}</li>
                            <li v-if="movieCard.original_language != ''"><span>Lingua:  </span><LangFlag :iso="movieCard.original_language"/>{{' ' + movieCard.original_language}}</li>
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
                            <li v-if="movieCard.overview"><span>Overview: </span>{{movieCard.overview}}</li>
                            <li v-else>Descrizione non disponibile</li>
                            <!--Fine overview-->
                                
                            <!--Inizio cast-->
                            <div>Actors:</div>
                            <li><span updateCast></span><span v-for="(actor, index) in 5" :key="index">{{cast[index].name}}, </span></li>
                            <!--Fine cast-->

                            <!--Inizio generi-->
                            <div>Genre:</div>
                            <li>
                                <span v-for="(genre, index) in movieCard.genre_ids" :key="index">
                                    <span v-for="(item, i) in genres" :key="i">
                                        <span v-if="(genre == item.id)">{{item.name}}, </span>
                                    </span>
                                </span>
                            </li>
                            <!--Fine generi-->
                        </div>
                    </div>
                    <!--Fine Info film-->               
                </div>          
            </div>
        </ul>
    </div>
</template>

<script>
import LangFlag from 'vue-lang-code-flags';

const axios = require('axios');

export default {
    name: 'filmCard',

    data(){
        return{
            imgUrl: 'https://image.tmdb.org/t/p/' + 'w342' + this.movieCard.poster_path,
            vote: Math.ceil(this.movieCard.vote_average / 2),
            id: this.movieCard.id,
            cast: [],
            genres: [],

            aaa: [],
            bbb: false,
            ccc:"",
            ddd: '',

            cardGenres:[]
        }
    },
    
    props:{
        'movieCard': Object,
        'genere': String
    },

    components:{
        LangFlag,
    },

    methods:{

        //Esegue chiamata API per membri del cast
        callCastApi: function(filmId){
            axios.get('https://api.themoviedb.org/3/movie/' + filmId +'/credits?api_key=918e2ad402623b3f2672adefc7b3a96f&language=en-US') 

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
            axios.get('https://api.themoviedb.org/3/genre/movie/list?api_key=918e2ad402623b3f2672adefc7b3a96f&language=en-US')

            .then((response) => {  
                this.genres = response.data.genres;
                this.Funzione()
                
            })
            
            .catch(function (error) {
                // handle error
                console.log(error);
            })
            return this.genres
        },

        
        Funzione(){
            this.movieCard.genre_ids.forEach(element => {
                    this.cardGenres.push(element)  
                });

                for(let i = 0; i < this.cardGenres.length; i++){
                    for(let j = 0; j < this.genres.length; j++){
                        if(this.cardGenres[i] == this.genres[j].id){
                            this.aaa.push(this.genres[j].name)
                        }
                    }
                }

                for(let x = 0; x < this.aaa.length; x ++){
                    if(this.aaa[x] == this.genere){
                        this.bbb = true
                    }
                    else{
                        this.bbb = false
                    }
                }

                return this.bbb
        }
        
        
    },

    //Richiama le due funzioni per la chiamata API al mounted
    mounted(){
        this.callCastApi(this.id)
        this.callGenres()  
         
    },

    computed:{

        miaFunzione(){
            
            let nuova = ''
            let toggle = false
            nuova = this.genere
            
            for(let i = 0; i < this.aaa.length; i++){
                if(nuova == this.aaa[i]){
                    toggle = true
                }
            }
            return toggle
        }      
    
        
    }
}
</script>

<style scoped lang="scss">
    //Importa stilizzazione grafica della singola card
    @import "../../assets/scss/cards.scss";
</style>

<!--:class="(miaFunzione == genere) ? '' : 'd-none' "-->