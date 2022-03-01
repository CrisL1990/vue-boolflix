<template>
    <div>
        <ul>
            <div class="img-cont position-relative">
                <li v-if="movieCard.poster_path"><img :src="imgUrl" alt=""></li>
                <li v-else><img class="img-fluid" src="../../assets/img/movie-clapboard.jpeg" alt=""></li>

                <div class="info-box position-absolute">
                    <li><span>Titolo: </span>{{movieCard.title}}</li>
                    <li><span>Titolo originale: </span>{{movieCard.original_title}}</li>
                    <li v-if="movieCard.original_language != ''"><span>Lingua: </span><LangFlag :iso="movieCard.original_language"/>{{' ' + movieCard.original_language}}</li>
                    <li>
                        <span>Voto: </span>
                        <span v-for="(number, i) in 5" :key="i"> 
                            <i :class="(number <= vote) ? 'fa-solid fa-star yellow' : 'fa-regular fa-star'"></i>
                        </span>
                    </li>
                    <li v-if="movieCard.overview"><span>Overview: </span>{{movieCard.overview}}</li>
                    <li v-else>Descrizione non disponibile</li>
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
    name: 'filmCard',

    data(){
        return{
            toggle: false,
            imgUrl: 'https://image.tmdb.org/t/p/' + 'w342' + this.movieCard.poster_path,
            vote: Math.ceil(this.movieCard.vote_average / 2) 
        }
    },

    props:{
        'movieCard': Object,
       
    },

    components:{
        LangFlag,
    },

}


</script>

<style scoped lang="scss">

    ul{
        color: white;
        list-style: none;
       
        li{
            margin: 15px 0;
        }

        .img-cont{
            height: 600px;

            &:hover .info-box{
                visibility: visible;
            }

            img{
                height: 600px;
                width: 100%;
                object-fit: cover;
               
            }
        }

        .info-box{
            top: 0;
            left: 0;
            height: 100%;
            width: 100%;
            background-color: rgba($color: #000000, $alpha: 0.8);
            padding: 0 30px;
            visibility: hidden;
        }

        
    }
    .yellow{
        color: rgb(255, 217, 0);
        
        
    }
</style>