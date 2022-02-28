<template>
    <header class="bg-dark d-flex justify-content-end align-items-center px-5">
        <form>
            <input v-model="search" type="text" name="" id="" class="mx-3">
            <button @click.prevent="searchTransfer">CLICCAMI!</button>
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
    }
</style>