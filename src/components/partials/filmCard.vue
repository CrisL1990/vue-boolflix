<template>
    <div>
        <ul>
            <div class="img-cont position-relative">
                <div class="flip-card-inner">

                    <div class="front">
                        <li v-if="movieCard.poster_path"><img :src="imgUrl" alt=""></li>
                        <li v-else><img class="img-fluid" src="../../assets/img/movie-clapboard.jpeg" alt=""></li>
                    </div>
                    
                    <div class="back" @click="callCastApi(id)">
                        <div class="info-box position-absolute">
                            <li><span>Titolo: </span>{{movieCard.title}}</li>
                            <li><span>Titolo originale: </span>{{movieCard.original_title}}</li>
                            <li v-if="movieCard.original_language != ''"><span>Lingua:  </span><LangFlag :iso="movieCard.original_language"/>{{' ' + movieCard.original_language}}</li>
                            <li>
                                <span>Voto: </span>
                                <span v-for="(number, i) in 5" :key="i"> 
                                    <i :class="(number <= vote) ? 'fa-solid fa-star yellow' : 'fa-regular fa-star'"></i>
                                </span>
                            </li>
                            <li v-if="movieCard.overview"><span>Overview: </span>{{movieCard.overview}}</li>
                            <li v-else>Descrizione non disponibile</li>
                            <div>Actors:</div>
                            <li><span updateCast></span><span v-for="(actor, index) in 5" :key="index">{{cast[index].name}}, </span></li>
                            
                        </div>
                    </div>               
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
            toggle: false,
            imgUrl: 'https://image.tmdb.org/t/p/' + 'w342' + this.movieCard.poster_path,
            vote: Math.ceil(this.movieCard.vote_average / 2),
            id: this.movieCard.id,
            cast: [],
        }
    },


    props:{
        'movieCard': Object,
       
    },


    components:{
        LangFlag,
    },

    
    methods:{

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
        }
    },

    mounted(){
        this.callCastApi(this.id)
    },
    
    
    computed:{

        
        updateCast(){

            return this.callCastApi(this.id)

            /*
            axios.get('https://api.themoviedb.org/3/movie/' + filmId +'/credits?api_key=918e2ad402623b3f2672adefc7b3a96f&language=en-US')
        
            .then((response) => {  
                this.cast = response.data.cast;
            })
            
            .catch(function (error) {
                // handle error
                console.log(error);
            })
            console.log(this.cast)
            return this.cast
            */
        }
        
    }   
    
}


</script>

<style scoped lang="scss">
    @import "../../assets/scss/cards.scss";
</style>