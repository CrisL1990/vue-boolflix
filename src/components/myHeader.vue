<template>
    <header class="d-flex justify-content-between align-items-center px-5">
        <div class="d-flex align-items-center" id="logo-container">
            <img src="../assets/img/netflix_logo.png" alt="">
        </div>

        <form>
            <input v-model="search" type="text" name="" placeholder="Search movie or serie" id="" class="mx-3">
            <button class="btn btn-danger" @click.prevent="searchTransfer">Search</button>
        </form>
        
    </header>
</template>

<script>
export default {
    name: 'myHeader',

    data(){
        return{
            search: "",
        }
        
    },

    methods:{

        searchTransfer(){
            this.$emit('searchFire', this.search);
        },
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