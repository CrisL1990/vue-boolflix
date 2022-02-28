<template>
    <div>
        <ul>
            <li><img :src="imgUrl" alt=""></li>
            <li>{{serieCard.name}}</li>
            <li>{{serieCard.original_name}}</li>
            <li>{{serieCard.original_language}}</li>
            <li v-if="serieCard.original_language != ''"><LangFlag :iso="serieCard.original_language"/></li>
            <li>{{serieCard.vote_average}}</li>
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
            imgUrl: 'https://image.tmdb.org/t/p/' + 'w780' + this.serieCard.backdrop_path,
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

<style>

</style>
