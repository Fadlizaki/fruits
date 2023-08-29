<template>
  <br>
  <br>
  <div class="bg-gray-100 py-8">
    <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex flex-col md:flex-row -mx-4">
        <div class="md:flex-1 px-4">
          <div class="h-[460px] rounded-lg bg-gray-300 mb-4">
            <img
              src="https://img.freepik.com/free-photo/many-different-berries-form-frame-white-background_485709-54.jpg?w=740&t=st=1693133987~exp=1693134587~hmac=313685f705004dbf64406d4b25540b8ee037e873b4ea3f345a13e732c1731bae" />
          </div>
        </div>
        <br>
        <br>
        <br>
        <br>
        <div class="md:flex-1 px-4">
          <h2 class="text-2xl font-bold mb-2">{{ products.name }}</h2>
          <p class="text-gray-600 text-sm mb-4">Kiwi adalah buah kecil yang berbentuk sawo.</p>
          <div class="mb-4">
            <button class="border rounded-md py-2 px-4 mr-2" @click="decrementQty">-</button>
            <input type="number" class="text-center w-20 border rounder-md py-2 px-2" v-model="number">
            <button class="border rounded-md py-2 px-4 ml-2" @click="incrementQty">+</button>
          </div>
          <div class="flex mb-4">
            <div class="mr-4">
              <span class="font-bold text-gray-700">Harga:</span>
              <span class="text-gray-600">Rp.{{ products.base_price * number }}</span>
            </div>
            <div>
              <span class="font-bold text-gray-700">Ketersediaan:</span>
              <span class="text-gray-600"> Tersedia</span>
            </div>
          </div>
          <div>
            <span class="font-bold text-gray-700">Deskripsi Produk dan manfaat:</span>
            <p class="text-gray-600 text-sm mt-2">
Menjaga tubuh tetap terhidrasi sangat penting untuk meningkatkan kesehatan pencernaan, metabolisme, kinerja otak, dan sel tubuh. Selain air putih, konsumsi buah-buahan dapat menjaga hidrasi tubuh. Salah satu buah lokal yang banyak mengandung air adalah semangka, kadar airnya hingga 92%
            </p>
          </div>
          <br>

          <div class="flex -mx-2 mb-4">
            <div v-if="token">
              <button class="px-3 py-2 bg-gray-800 text-white text-xs font-bold uppercase rounded" type="button"
                @click="addKeranjang({ variation_id: products.variations[0].id, qty: number })">tambah ke keranjang</button>
            </div>
            <div v-else>
              <router-link to="/login">
                <button class="px-3 py-2 bg-gray-800 text-white text-xs font-bold uppercase rounded" type="button"
                  @click="addKeranjang({ variation_id: products.variations[0].id, qty: number })">tambah ke keranjang</button>
              </router-link>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters, mapActions } from "vuex";

export default {
  data() {
    return {
      token: null,
      number: 1
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



    decrementQty() {
      if (this.number > 1) {
        this.number--;
      }
    },

    incrementQty() {
      this.number++;
    },
    ...mapActions("product", ["addKeranjang"]),
  },
  beforeMount() {
    this.fetchProduk()
    this.fetchKeranjang()

  },
  mounted() {
    const Slug = this.$route.params.slug;
    this.fetchSingleProduk(Slug)

    //cek token
    const cektoken = localStorage.getItem('token');
    this.token = cektoken
  }


};
</script>