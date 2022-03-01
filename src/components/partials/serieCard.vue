<template>
    <div>
        <ul>
            <div class="img-cont position-relative">
                <div class="flip-card-inner">

                    <div class="front">
                        <li v-if="serieCard.poster_path"><img :src="imgUrl" alt=""></li>
                        <li v-else><img class="img-fluid" src="../../assets/img/movie-clapboard.jpeg" alt=""></li>
                    </div>

                    <div class="back">
                        <div class="info-box position-absolute">
                        <li><span>Titolo: </span>{{serieCard.name}}</li>
                        <li><span>Titolo originale: </span>{{serieCard.original_name}}</li>
                        <li v-if="serieCard.original_language != ''"><span>Lingua: </span><LangFlag :iso="serieCard.original_language"/>{{' ' + serieCard.original_language}}</li>
                        <li>
                            <span>Voto: </span>
                            <span v-for="(number, i) in 5" :key="i">
                                <i :class="(number <= vote) ? 'fa-solid fa-star yellow' : 'fa-regular fa-star'"></i>
                            </span>
                        </li>
                        <li v-if="serieCard.overview"><span>Overview: </span>{{serieCard.overview}}</li>
                        <li v-else>Descrizione non disponibile</li>
                </div>
                    </div>

                </div>
                

                
            </div>
            
            <!--
            
            -->
        </ul>
    </div>
</template>

<script>
import LangFlag from 'vue-lang-code-flags';
export default {
    name: 'serieCard',

    data(){
        return{
            toggle: false,
            imgUrl: 'https://image.tmdb.org/t/p/' + 'w342' + this.serieCard.poster_path,
            vote: Math.ceil(this.serieCard.vote_average / 2),
            
        }
    },

    props:{
        'serieCard': Object,
      
    },


    components:{
        LangFlag,
    },

}


</script>

<style scoped lang="scss">
    @import "../../assets/scss/cards.scss";
</style>


