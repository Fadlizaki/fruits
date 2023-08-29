<template>
  <div class="flex flex-col justify-center items-center min-h-screen">
    <div class="bg-gray-100 rounded-lg shadow-lg p-6">
        <h1 class="text-2xl font-bold mb-6">Keranjang Belanja</h1>
        <div class="flex justify-between mb-4" v-for="cart in getKeranjang" :key="cart.id">
            <div class="flex items-center">
              <img
                src="https://img.freepik.com/free-photo/many-different-berries-form-frame-white-background_485709-54.jpg?w=740&t=st=1693133987~exp=1693134587~hmac=313685f705004dbf64406d4b25540b8ee037e873b4ea3f345a13e732c1731bae"
                alt="" class="h-20 w-20" />
                <div>
                    <h2 class="font-bold">{{ cart.name }}</h2>
                    <p class="text-gray-700">{{ cart.cart_id }}</p>
                </div>
            </div>
            <div class="flex items-center">
                <button class="text-red-500 hover:text-red-700"><i class="fas fa-trash"></i></button>
                <div class="mx-4">
                  <span
                      class="cursor-pointer rounded-l bg-gray-100 py-1 px-3 duration-100 hover:bg-red-500 hover:text-blue-50"
                      @click="editKeranjang({ cart_id: cart.cart_id, type: 'minus' })"> - </span>
                    <span class="h-2 w-2 border bg-white text-center text-xs outline-none" type="number" value="2"
                      min="1">{{ cart.qty }} </span>
                    <span
                      class="cursor-pointer rounded-r bg-gray-100 py-1 px-3 duration-100 hover:bg-blue-500 hover:text-blue-50"
                      @click="editKeranjang({ cart_id: cart.cart_id, type: 'plus' })"> + </span>
                      <button class="text-gray-600 transition hover:text-red-600" @click="deleteKeranjang(cart.cart_id)">
                  <span class="sr-only">Remove item</span>

                  <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                    stroke="currentColor" class="h-4 w-4">
                    <path stroke-linecap="round" stroke-linejoin="round"
                      d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0" />
                  </svg>
                </button>
                </div>
                
                <span class="font-bold">Rp.{{ cart.regular_price }}</span>
            </div>
        </div>
        <hr class="my-4">
        <div class="flex justify-between items-center">
            <span class="font-bold">Total:</span>
            <span class="font-bold">{{ totalHarga() }}</span>
        </div>
        <div class="flex justify-center mt-6">
          <a href="checkout">
            <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">Checkout</button>
            </a>
        </div>
    </div>
</div>
</template>
<script>
import { mapGetters, mapActions } from 'vuex';

export default {
  data(){
    return{
      number : 0
    }
  },
    computed: {
        ...mapGetters('keranjang', ['getKeranjang','getAddress']),
        
    },
    methods: {
        ...mapActions('keranjang', ['fetchKeranjang','deleteKeranjang','editKeranjang','fetchAddress']),

        totalHarga() {
            this.total = this.getKeranjang.reduce((acc, cart) => {
                return acc + parseFloat(cart.regular_price * cart.qty);
            }, 0);
            return this.total.toFixed();
        },

    },
    created() {
        this.fetchKeranjang();
        this.fetchAddress();
      
    }
}
</script>