<template>
    <div>
        <ul>
            <li><img :src="imgUrl" alt=""></li>
            <li>{{serieCard.name}}</li>
            <li>{{serieCard.original_name}}</li>
            <li v-if="serieCard.original_language != ''"><LangFlag :iso="serieCard.original_language"/>{{' ' + serieCard.original_language}}</li>
            <li>
                <i :class="(serieCard.vote_average >= 0) ? 'yellow' : '' " class="fa-regular fa-star"></i>
                <i :class="(serieCard.vote_average >= 2) ? 'yellow' : '' " class="fa-regular fa-star"></i>
                <i :class="(serieCard.vote_average >= 4) ? 'yellow' : '' " class="fa-regular fa-star"></i>
                <i :class="(serieCard.vote_average >= 6) ? 'yellow' : '' " class="fa-regular fa-star"></i>
                <i :class="(serieCard.vote_average >= 8) ? 'yellow' : '' " class="fa-regular fa-star"></i>
            </li>
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
            imgUrl: 'https://image.tmdb.org/t/p/' + 'w342' + this.serieCard.backdrop_path,
        }
    },

    props:{
        'serieCard': Object
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
