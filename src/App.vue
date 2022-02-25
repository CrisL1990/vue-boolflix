<template>
  <div id="app">
      <myHeader @searchFire='setKeyword'/>
      <myMain :movieCards="movies" :searching="flag"/>
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
        prefix: "https://api.themoviedb.org/3/search/movie?api_key=",
        myKey: "918e2ad402623b3f2672adefc7b3a96f",
        query: "&query=",
        wordToSearch: "",

        endPoint: "",
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
          this.endPoint = this.prefix + this.myKey + this.query + this.wordToSearch ;
          console.log(this.endPoint);

          this.callApi();
      },

      callApi(){
           
          axios.get(this.endPoint)
        
          .then((response) => {  
              this.movies = response.data.results;
              this.allResults = [...this.movies, ...this.series];
              this.flag = true;
              console.log(this.movies);

          })
           
          .catch(function (error) {
              // handle error
              console.log(error);
          })
        
        }
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
