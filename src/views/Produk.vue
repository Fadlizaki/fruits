<template>
    <div v-if="getProduk == false">
        <div class="h-screen bg-white">
            <div class="flex justify-center items-center h-full">
                <img class="h-16 w-16" src="https://icons8.com/preloaders/preloaders/1488/Iphone-spinner-2.gif" alt="">
            </div>
        </div>
    </div>
    <div v-else>
        <br>
        <br>
        <br>
        <br>
        <header class="text-center">
            <h1 class="text-xl font-bold text-gray-900 sm:text-3xl">Product</h1>
        </header>
        <br>
        <div class="flex flex-wrap items-center justify-center">
            <!-- <div class="grid md:grid-cols-3 gap-8  mt-10 pl-5"></div> -->
            <div v-for="product in getProduk" :key="product.slug">

                <div class="flex-shrink-0 m-6 relative overflow-hidden bg-orange-500 rounded-lg max-w-xs shadow-lg">
                    <svg class="absolute bottom-0 left-0 mb-8" viewBox="0 0 375 283" fill="none"
                        style="transform: scale(1.5); opacity: 0.1;">
                        <rect x="159.52" y="175" width="152" height="152" rx="8" transform="rotate(-45 159.52 175)"
                            fill="white" />
                        <rect y="107.48" width="152" height="152" rx="8" transform="rotate(-45 0 107.48)" fill="white" />
                    </svg>
                    <div class="relative pt-10 px-10 flex items-center justify-center">
                        <div class="block absolute w-48 h-48 bottom-0 left-0 -mb-24 ml-3"
                            style="background: radial-gradient(black, transparent 60%); transform: rotate3d(0, 0, 1, 20deg) scale3d(1, 0.6, 1); opacity: 0.2;">
                        </div>
                        <img class="relative w-40"
                            src="../assets/pngwing.com.png"
                            alt="">
                    </div>
                    <div class="relative text-white px-6 pb-6 mt-6">
                        <span class="block opacity-75 -mb-1">{{ product.name }}</span>
                        <div class="flex justify-between">
                            <span class="block font-semibold text-xl"></span>
                            <router-link :to="{ name: 'SingleProduk', params: { slug: product.slug } }">
                                <span
                                    class="block bg-white rounded-full text-teal-500 text-xs font-bold px-3 py-2 leading-none flex items-center">Rp.{{
                                        product.base_price }}</span>
                            </router-link>
                        </div>
                    </div>
                </div>


            </div>
        </div>
    </div>
</template>
<script>
import { mapGetters, mapActions } from 'vuex';

export default {
    computed: {
        ...mapGetters('product', ['getProduk']),
    },
    methods: {
        ...mapActions('product', ['fetchProduk']),
    },
    created() {
        this.fetchProduk();
    }
}
</script>