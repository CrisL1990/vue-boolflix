<template>
    <div>
        <ul>
            <li>{{serieCard.name}}</li>
            <li>{{serieCard.original_name}}</li>
            <li>{{serieCard.original_language}}</li>
            <li>{{serieCard.vote_average}}</li>
        </ul>
    </div>
</template>

<script>

export default {
    name: 'serieCard',

    data(){
        return{
            toggle: false,
        }
    },

    props:{
        'serieCard': Object
    },

    components:{
    
    },
}


</script>

<style>

</style>
