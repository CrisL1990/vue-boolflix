<template>
    <main>
        <ul v-for="(movie, index) in movies" :key="index">
            <li>{{movie.original_title}}</li>
        </ul>
    </main>
</template>

<script>
export default {
    name: 'myMain',

    data(){
        return{
            props:{
                movies: Object,
            }
        }
    }
}
</script>

<style scoped lang="scss">

</style>