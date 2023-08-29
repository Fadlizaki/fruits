<template>
     <br>
    <br>
    <br>
    <br>
    <div v-if="getcategory == false">
        <div class="h-screen bg-white">
            <div class="flex justify-center items-center h-full">
                <img class="h-16 w-16" src="https://icons8.com/preloaders/preloaders/1488/Iphone-spinner-2.gif" alt="">
            </div>
        </div>
    </div>
    <header class="text-center">
        <h1 class="text-xl font-bold text-gray-900 sm:text-3xl">Categori</h1>
    </header>
    <div class="flex flex-wrap items-center justify-center">

        <div v-for="category in getcategory">


            <div class="relative m-8 w-full max-w-xs overflow-hidden rounded-lg bg-white shadow-md relative px-6 pb-6 mt-6">
                <img :src="category.banner" alt="">
                <h1> {{ category.name }} </h1>


            </div>
        </div>
    </div>
</template>
<script>
import { mapGetters, mapActions } from 'vuex';
    
    export default {
        computed: {
            ...mapGetters('category', ['getcategory']),
        },
        methods: {
            ...mapActions('category', ['fetchCategory']),
    },
    created(){
        this.fetchCategory();
    }
}
</script>