<template>
    <div>
        <ul>
            <li><img :src="imgUrl" alt=""></li>
            <li>{{movieCard.title}}</li>
            <li>{{movieCard.original_title}}</li>
            <li v-if="movieCard.original_language != ''"><LangFlag :iso="movieCard.original_language"/></li>
            <li>{{movieCard.vote_average}}</li>
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
            imgUrl: 'https://image.tmdb.org/t/p/' + 'w780' + this.movieCard.backdrop_path,
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

<style>

</style>


<!--  (item.visible == false) ? 'hide' : '' "  -->