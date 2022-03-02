<template>
    <header class="d-flex justify-content-between align-items-center px-5">
        <div class="d-flex align-items-center" id="logo-container">
            <img src="../assets/img/netflix_logo.png" alt="">
        </div>

        <form>
            <input v-model="search" type="text" name="" placeholder="Search movie or serie" id="" class="mx-3">

            <select @change="$emit('changeGenre', selected)" v-model="selected" class="mx-3" name="Select genre" id="">
                <option :value="genre.name" v-for="(genre, index) in genresMovie" :key="index">{{genre.name}}</option>
            </select>

            <button class="btn btn-danger" @click.prevent="searchTransfer">Search</button>
        </form>
        
    </header>
</template>

<script>

const axios = require('axios');

export default {
    name: 'myHeader',

    data(){
        return{
            search: "",
            genresMovie: [],
            selected: ""
        }
        
    },

    methods:{

        searchTransfer(){
            this.$emit('searchFire', this.search);
        },

        callGenresMovie: function(){
            axios.get('https://api.themoviedb.org/3/genre/movie/list?api_key=918e2ad402623b3f2672adefc7b3a96f&language=en-US')

            .then((response) => {  
                this.genresMovie = response.data.genres;
            })
            
            .catch(function (error) {
                // handle error
                console.log(error);
            })
            console.log(this.genresMovie)

            return this.genresMovie
        },

        prova(){
            this.selectetGenre = this.genresMovie.name
           
        }
    }, 
    
    mounted(){
        this.callGenresMovie()
    }
}
</script>

<style scoped lang="scss">
    header{
        height: 100px;
        width: 100%;
        background-color: black;

        #logo-container{
            height: 120px;

            img{
                height: 80px;
            }
        }
    }
</style>