<template>
  <div id="app">
      <myHeader @searchFire='setKeyword'/>
      <myMain :movies="result"/>
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
        prefix: "https://api.themoviedb.org/3/movie/550?api_key=",
        myKey: "918e2ad402623b3f2672adefc7b3a96f",
        query: "&query=",
        wordToSearch: "",

        endPoint: "",

        result: {}
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

          this.callApi();
      },

      callApi(){
           
          axios.get(this.endPoint)
        
          .then((response) => {  
              this.result = response.data;
              console.log(this.result);

          })
           
          .catch(function (error) {
              // handle error
              console.log(error);
          })
        
        }
    }
  }
</script>

<style lang="scss">

</style>
