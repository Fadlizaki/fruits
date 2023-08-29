<template>
  <!-- component -->
  <br>
  <br>
  <br>
  <br>
  <br>
  <div v-if="products">
    <div class="py-6 flex justify-center items-center h-full">
      <div class="flex max-w-md bg-white shadow-lg rounded-lg overflow-hidden">
        <div class="w-1/3 bg-cover"
          style="background-image: url('https://img.freepik.com/free-photo/group-fruits-including-mango-mango-avocado_1340-31387.jpg?t=st=1693134312~exp=1693137912~hmac=9d89a931123f3f81d4c3e745451a140eba52e642d7c510c74d4697a0f386a38b&w=740')">
        </div>
        <div class="w-2/3 p-4">
          <h1 class="text-gray-900 font-bold text-2xl">{{ products.name }}</h1>
          <p class="mt-2 text-gray-600 text-sm">Lorem ipsum dolor sit amet consectetur adipisicing elit In odit
            exercitationem fuga id nam quia</p>
          <div class="flex item-center mt-2">
              <button class="border rounded-md py-2 px-4 mr-2" @click="decrementQty">-</button>
              <input type="number" class="text-center w-20 border rounder-md py-2 px-2" v-model="number">
              <button class="border rounded-md py-2 px-4 ml-2" @click="incrementQty">+</button>
          </div>
          <div class="flex item-center justify-between mt-3">
            <h1 class="text-gray-700 font-bold text-xl">Rp.{{ products.base_price * number }}</h1>
            <div v-if="token">
              <button class="px-3 py-2 bg-gray-800 text-white text-xs font-bold uppercase rounded" type="button"
                @click="addKeranjang({ variation_id: products.variations[0].id, qty: number })">Add to Cart</button>
            </div>
            <div v-else>
              <router-link to="/login">
                <button class="px-3 py-2 bg-gray-800 text-white text-xs font-bold uppercase rounded" type="button"
                  @click="addKeranjang({ variation_id: products.variations[0].id, qty: number })">Add to Cart</button>
              </router-link>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <br>
  <br>
  <br>
  <br>
</template>

<script>
import { mapGetters, mapActions } from "vuex";

export default {
  data(){
    return {
      token : null,
      number : 1
    }
  },
  computed: {
    ...mapGetters("product", ["getProdukSlug"]),
    products() {
      return this.getProdukSlug(this.$route.params.slug);
    },
  },
  methods: {
    ...mapActions("product", ["fetchSingleProduk"]),
    ...mapActions("product", ["fetchProduk"]),
    ...mapActions("keranjang", ["fetchKeranjang",]),
    

    
    decrementQty(){
      if(this.number > 1){
      this.number--;
      }
    },

    incrementQty(){
      this.number++;
    },
    ...mapActions("product",["addKeranjang"]),
  },
  beforeMount() {
    this.fetchProduk()
    this.fetchKeranjang()
   
  },
  mounted(){
      const Slug = this.$route.params.slug;
      this.fetchSingleProduk(Slug)
      
      //cek token
      const cektoken = localStorage.getItem('token');
      this.token = cektoken
    }


};
</script>