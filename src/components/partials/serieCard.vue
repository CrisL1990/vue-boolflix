<template>
    <div>
        <ul>
            <div class="img-cont position-relative">
                <li v-if="serieCard.poster_path"><img :src="imgUrl" alt=""></li>
                <li v-else><img class="img-fluid" src="../../assets/img/movie-clapboard.jpeg" alt=""></li>

                <div class="info-box position-absolute">
                    <li>{{serieCard.name}}</li>
                    <li>{{serieCard.original_name}}</li>
                    <li v-if="serieCard.original_language != ''"><LangFlag :iso="serieCard.original_language"/>{{' ' + serieCard.original_language}}</li>
                    <li>
                        <span v-for="(number, i) in 5" :key="i">
                            <i :class="(number <= vote) ? 'fa-solid fa-star yellow' : 'fa-regular fa-star'"></i>
                        </span>
                    </li>
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

   ul{
        color: white;
        list-style: none;
       

        .img-cont{
            height: 600px;

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
        }

        
    }
    .yellow{
        color: rgb(255, 217, 0);
    }

</style>


