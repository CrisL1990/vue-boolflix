<template>
    <div>
        <ul>
            <li><img :src="imgUrl" alt=""></li>
            <li>{{movieCard.title}}</li>
            <li>{{movieCard.original_title}}</li>
            <li v-if="movieCard.original_language != ''"><LangFlag :iso="movieCard.original_language"/>{{' ' + movieCard.original_language}}</li>

            <li>
                <i :class="(movieCard.vote_average >= 0) ? 'yellow' : '' " class="fa-regular fa-star"></i>
                <i :class="(movieCard.vote_average >= 2) ? 'yellow' : '' " class="fa-regular fa-star"></i>
                <i :class="(movieCard.vote_average >= 4) ? 'yellow' : '' " class="fa-regular fa-star"></i>
                <i :class="(movieCard.vote_average >= 6) ? 'yellow' : '' " class="fa-regular fa-star"></i>
                <i :class="(movieCard.vote_average >= 8) ? 'yellow' : '' " class="fa-regular fa-star"></i>
            </li>
            
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
            imgSize: 'w780',
            imgUrl: 'https://image.tmdb.org/t/p/' + 'w342' + this.movieCard.backdrop_path,
        }
    },

    props:{
        'movieCard': Object
    },

    components:{
        LangFlag,
    },
}


</script>

<style scoped lang="scss">
    .yellow{
        color: yellow;
        
    }
</style>


<!--  (item.visible == false) ? 'hide' : '' "  -->