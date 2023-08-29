<template>

  <div class="pt-20 bg-gray">
    <div class="mx-auto max-w-screen-xl px-4 py-8 sm:px-6 sm:py-12 lg:px-8">
      <div class="mx-auto max-w-3xl">
        <header class="text-center">
          <h1 class="text-xl font-bold text-gray-900 sm:text-3xl">Cart</h1>
        </header>

        <div class="mt-8">
          <ul class="space-y-4" v-for="cart in getKeranjang" :key="cart.id">

            <li class="flex items-center gap-4">
              <img
                src="https://img.freepik.com/free-photo/many-different-berries-form-frame-white-background_485709-54.jpg?w=740&t=st=1693133987~exp=1693134587~hmac=313685f705004dbf64406d4b25540b8ee037e873b4ea3f345a13e732c1731bae"
                alt="" class="h-16 w-16 rounded object-cover" />

              <div>
                <h3 class="text-sm text-gray-900">{{ cart.name }}</h3>

                <dl class="mt-0.5 space-y-px text-[10px] text-gray-600">
                  <div>
                    <dt class="inline">Id:</dt>
                    <dd class="inline">{{ cart.cart_id }}</dd>
                  </div>

                  <div>
                    <dt class="inline">Harga:</dt>
                    <dd class="inline">Rp.{{ cart.regular_price }}</dd>
                  </div>
                </dl>
              </div>

              <div class="flex flex-1 items-center justify-end gap-2">
                <form>


                  <!-- <input
                  type="number"
                  min="1"
                  value="1"
                  id="Line3Qty"
                  class="h-8 w-12 rounded border-gray-200 bg-gray-50 p-0 text-center text-xs text-gray-600 [-moz-appearance:_textfield] focus:outline-none [&::-webkit-inner-spin-button]:m-0 [&::-webkit-inner-spin-button]:appearance-none [&::-webkit-outer-spin-button]:m-0 [&::-webkit-outer-spin-button]:appearance-none"
                /> -->
                  <div class="flex items-center border-gray-100">
                    <span
                      class="cursor-pointer rounded-l bg-gray-100 py-1 px-3.5 duration-100 hover:bg-blue-500 hover:text-blue-50"
                      @click="editKeranjang({ cart_id: cart.cart_id, type: 'minus' })"> - </span>
                    <span class="h-8 w-8 border bg-white text-center text-xs outline-none" type="number" value="2"
                      min="1">{{ cart.qty }} </span>
                    <span
                      class="cursor-pointer rounded-r bg-gray-100 py-1 px-3 duration-100 hover:bg-blue-500 hover:text-blue-50"
                      @click="editKeranjang({ cart_id: cart.cart_id, type: 'plus' })"> + </span>
                  </div>
                </form>

                <button class="text-gray-600 transition hover:text-red-600" @click="deleteKeranjang(cart.cart_id)">
                  <span class="sr-only">Remove item</span>

                  <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                    stroke="currentColor" class="h-4 w-4">
                    <path stroke-linecap="round" stroke-linejoin="round"
                      d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0" />
                  </svg>
                </button>
              </div>
            </li>
          </ul>

          <div class="mt-8 flex justify-end border-t border-gray-100 pt-8">
            <div class="w-screen max-w-lg space-y-4">
              <dl class="space-y-0.5 text-sm text-gray-700">
                <!-- <div class="flex justify-between">
                  <dt>Subtotal</dt>
                  <dd>{{ totalharga }}</dd>
                </div> -->

                <!-- <div class="flex justify-between">
                  <dt>Q</dt>
                  <dd>{{ diskon }}</dd>
                </div> -->

                <div class="flex justify-between !text-base font-medium">
                  <dt>Total</dt>
                  <dd>{{ totalHarga() }}</dd>
                </div>
              </dl>

              <div class="flex justify-end">
                <a href="checkout"
                  class="block rounded bg-gray-700 px-5 py-3 text-sm text-gray-100 transition hover:bg-gray-600">
                  Checkout
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div >
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