<template>
  <div id="app">
      <myHeader @searchFire='setKeyword'/>
      <myMain />
  </div>
</template>

<script>

  import myHeader from './components/myHeader.vue';
  import myMain from './components/myMain.vue';

  export default {
    name: 'App',

    data(){
      return{
        wordToSearch: "",
      }
    },

    components:{
      myHeader,
      myMain
    },

    methods:{

      setKeyword(keyword){
          this.wordToSearch = keyword;
          console.log(this.wordToSearch);
      }
    }
  }
</script>

<style lang="scss">

</style>
