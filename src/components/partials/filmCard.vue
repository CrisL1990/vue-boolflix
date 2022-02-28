<template>
    <div>
        <ul>
            <li>{{movieCard.title}}</li>
            <li>{{movieCard.original_title}}</li>
            <li><LangFlag :iso="movieCard.original_language"/></li>
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