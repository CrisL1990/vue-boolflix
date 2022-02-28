<template>
  <div id="app">
      <myHeader @searchFire='setKeyword'/>
      <myMain :movieCards="movies" :serieCards="series" :searching="flag"/>
  </div>
</template>

<script>

  import myHeader from './components/myHeader.vue';
  import myMain from './components/myMain.vue';

  const axios = require('axios');
  
  export default {
    name: 'App',

    data(){
      return{
        prefixFilm: "https://api.themoviedb.org/3/search/movie?api_key=",
        prefixSerie: "https://api.themoviedb.org/3/search/tv?api_key=",
        myKey: "918e2ad402623b3f2672adefc7b3a96f",
        query: "&query=",
        wordToSearch: "",

        FilmEndPoint: "",
        serieEndPoint: "",

        flag: false,
        
        movies: [],
        series: []
      }
    },

    components:{
      myHeader,
      myMain
    },

    methods:{

      setKeyword(keyword){

          this.wordToSearch = keyword;
          
          this.FilmEndPoint = this.prefixFilm + this.myKey + this.query + this.wordToSearch ;
          this.serieEndPoint = this.prefixSerie + this.myKey + this.query + this.wordToSearch ;
         
          this.callApiFilm();
          this.callApiSerie();
          
      },

      callApiFilm(){
           
          axios.get(this.FilmEndPoint)
        
          .then((response) => {  
              this.movies = response.data.results;
              this.allResults = [...this.movies, ...this.series];
              this.flag = true;
          })
           
          .catch(function (error) {
              // handle error
              console.log(error);
          })
        
        }
      },

      callApiSerie(){
           axios.get(this.serieEndPoint)
        
          .then((response) => {  
              this.series = response.data.results;
              this.flag = true;
          })
           
          .catch(function (error) {
              // handle error
              console.log(error);
          })
        
      },

    computed:{
      computedResults: function(){
        return [...this.movies];
      }
    }
  }
</script>

<style lang="scss">

</style>
