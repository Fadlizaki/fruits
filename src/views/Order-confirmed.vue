<template>
  <div class="pt-20 bg-gray-100">
    <div class="container mx-auto px-4">
      <div class="flex flex-wrap items-center justify-center">
    <div class=" flex-shrink-0 m-8 overflow-hidden bg-red-500 rounded-lg  shadow-lg">
      <div
        class="block rounded-lg bg-white text-center shadow-[0_2px_15px_-3px_rgba(0,0,0,0.07),0_10px_20px_-2px_rgba(0,0,0,0.04)] dark:bg-neutral-700 ">
        <div class="border-b-2 border-neutral-100 px-6 py-3 dark:border-neutral-600 dark:text-neutral-50">
          <!-- Featured -->
          <h1 class="text-3xl font-bold pt-10">Terimakasih Telah Memesan</h1>
          <p>Kode Pemesanan : {{ getOrder.code }}</p>
          <p class="italic">
            Terimakasih atas kepercayaan Tn./Ny. {{ getOrder.user.name }}
          </p>
        </div>
        <div class="p-6">
          <!-- <h5
      class="mb-2 text-xl font-medium leading-tight text-neutral-800 dark:text-neutral-50">
      Special title treatment
    </h5>
    <p class="mb-4 text-base text-neutral-600 dark:text-neutral-200">
      With supporting text below as a natural lead-in to additional
      content.
    </p> -->
          <div>
            <dl class="max-w-md text-gray-900 divide-y divide-gray-200 dark:text-white dark:divide-gray-700">
              <div class="flex flex-col pb-3">
                <dt class="mb-1 text-black md:text-lg dark:text-black">
                  Kode Pemesanan :
                </dt>
                <dd class="text-lg font-semibold">{{ getOrder.code }}</dd>
              </div>
              <div class="flex flex-col pb-3">
                <dt class="mb-1 text-black md:text-lg dark:text-black">
                  Alamat Email :
                </dt>
                <dd class="text-lg font-semibold">{{ getOrder.user.email }}</dd>
              </div>
              <div class="flex flex-col py-3">
                <dt class="mb-1 text-black md:text-lg dark:text-black">
                  Alamat Rumah :
                </dt>
                <dd class="text-lg font-semibold">
                  {{ getOrder.shipping_address.address }},
                  {{ getOrder.shipping_address.city }},
                  {{ getOrder.shipping_address.state }},
                  {{ getOrder.shipping_address.country }},
                  {{ getOrder.shipping_address.postal_code }}
                </dd>
              </div>
              <div class="flex flex-col pt-3">
                <dt class="mb-1 text-black md:text-lg dark:text-black">
                  Nomor Telpon :
                </dt>
                <dd class="text-lg font-semibold">
                  {{ getOrder.shipping_address.phone }}
                </dd>
              </div>
            </dl>
          </div>

        </div>
        <div>
          <dl class="max-w-md text-gray-900 divide-y divide-gray-200 dark:text-white dark:divide-gray-700">
            <div class="flex flex-col pb-3">
              <dt class="mb-1 text-black md:text-lg dark:text-black">
                Metode Pembayaran :
              </dt>
              <dd class="text-lg font-semibold">
                {{ getOrder.orders[0].payment_type }}
              </dd>
            </div>
            <div class="flex flex-col pb-3">
              <dt class="mb-1 text-black md:text-lg dark:text-black">
                Metode Pengiriman :
              </dt>
              <dd class="text-lg font-semibold">
                {{ getOrder.orders[0].delivery_type }}
              </dd>
            </div>
            <div class="flex flex-col py-3">
              <dt class="mb-1 text-black md:text-lg dark:text-black">
                Alamat Tagihan :
              </dt>
              <dd class="text-lg font-semibold">
                {{ getOrder.shipping_address.address }},
                {{ getOrder.shipping_address.city }},
                {{ getOrder.shipping_address.state }},
                {{ getOrder.shipping_address.country }},
                {{ getOrder.shipping_address.postal_code }}
              </dd>
            </div>
            <div class="flex flex-col pt-3">
              <dt class="mb-1 text-black md:text-lg dark:text-black">
                Total Barang :
              </dt>
              <dd class="text-lg font-semibold">
                {{ getOrder.orders[0].grand_total }}
              </dd>
            </div>
          </dl>
        </div>
        <div class="relative overflow-x-auto pt-10 ">
        <table class="w-full text-sm text-left text-gray-500 dark:text-gray-400">
          <thead class="text-xs text-gray-800 uppercase bg-red-600 dark:bg-gray-800 dark:text-gray-800">
            <tr>
              <th scope="col" class="px-6 py-3">No.</th>
              <th scope="col" class="px-6 py-3">Product</th>
              <th scope="col" class="px-6 py-3">Quantity</th>
              <th scope="col" class="px-6 py-3">Price</th>
            </tr>
          </thead>
          <tbody>
            <tr class="bg-white border-b dark:bg-gray-900 dark:border-gray-900 text-gray-900 "
              v-for="(order, index) in getOrder.orders[0].products.data">
              <th scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                {{ index + 1 }}
              </th>
              <td class="px-6 py-4">{{ order.name }}</td>
              <td class="px-6 py-4">{{ order.quantity }}</td>
              <td class="px-6 py-4">{{ order.total }}</td>
            </tr>
          </tbody>
        </table>
        <div class="mt-6 border-t border-b py-2">
          <div class="flex items-center justify-between">
            <p class="text-sm font-medium text-gray-900">Total Belanja</p>
            <p class="font-semibold text-gray-900">Rp. {{ getOrder.grand_total }}</p>
          </div>
          <div class="flex items-center justify-between">
            <p class="text-sm font-medium text-gray-900">Biaya Jasa</p>
            <p class="font-semibold text-gray-900">

            </p>
          </div>
        </div>
        <div class="mt-6 flex items-center justify-between">
          <p class="text-sm font-medium text-gray-900">Total Harga : </p>
          <p class="text-2xl font-semibold text-gray-900">
            Rp. {{ (getOrder.grand_total) }}
          </p>
        </div>
        <br>
      </div>
        <div class="border-t-2 border-neutral-100 px-6 py-3 dark:border-neutral-600 dark:text-neutral-50">
          <button type="button"
            class="inline-block rounded bg-primary px-6 pb-2 pt-2.5 text-xs font-medium uppercase leading-normal text-white shadow-[0_4px_9px_-4px_#3b71ca] transition duration-150 ease-in-out hover:bg-primary-600 hover:shadow-[0_8px_9px_-4px_rgba(59,113,202,0.3),0_4px_18px_0_rgba(59,113,202,0.2)] focus:bg-primary-600 focus:shadow-[0_8px_9px_-4px_rgba(59,113,202,0.3),0_4px_18px_0_rgba(59,113,202,0.2)] focus:outline-none focus:ring-0 active:bg-primary-700 active:shadow-[0_8px_9px_-4px_rgba(59,113,202,0.3),0_4px_18px_0_rgba(59,113,202,0.2)] dark:shadow-[0_4px_9px_-4px_rgba(59,113,202,0.5)] dark:hover:shadow-[0_8px_9px_-4px_rgba(59,113,202,0.2),0_4px_18px_0_rgba(59,113,202,0.1)] dark:focus:shadow-[0_8px_9px_-4px_rgba(59,113,202,0.2),0_4px_18px_0_rgba(59,113,202,0.1)] dark:active:shadow-[0_8px_9px_-4px_rgba(59,113,202,0.2),0_4px_18px_0_rgba(59,113,202,0.1)]"
            data-te-ripple-init data-te-ripple-color="light">
            Button
          </button>
        </div>
      </div>
    </div>
  </div>
    </div>
  </div>
</template>

<script>
import { mapGetters, mapState } from 'vuex';
export default {
  props: ['orderCode'],
  computed: {
    ...mapGetters('order', ['getOrder']),
  },
  created() {
    this.$store.dispatch('order/fetchOrderData', this.orderCode);
  },
};
</script>