<template>
<br>
<br>
<br>
  <div class="bg-white border rounded-lg shadow-lg px-6 py-8 max-w-md mx-auto mt-8" >
    <h1 class="font-bold text-2xl my-4 text-center text-blue-600">Terimakasih Telah Memesan</h1>
    <p class="italic text-center">
            Terimakasih atas kepercayaan Tn./Ny. {{ getOrder.user.name }}
          </p>
    <hr class="mb-2">
    <div class="flex justify-between mb-6">
        <h1 class="text-lg font-bold">Faktur</h1>
        <div class="text-gray-700">
            <div>Date: 01/05/2023</div>
            <div>{{ getOrder.code }}</div>
        </div>
    </div>
    <div class="mb-8">
        <h2 class="text-lg font-bold mb-4">Pembayaran kepada:</h2>
        <div class="text-gray-700 mb-2">{{ getOrder.user.name }}</div>
        <div class="text-gray-700 mb-2"> {{ getOrder.shipping_address.address }},{{ getOrder.shipping_address.city }}, {{ getOrder.shipping_address.state }}</div>
        <div class="text-gray-700 mb-2"> {{ getOrder.shipping_address.country }},
                  {{ getOrder.shipping_address.postal_code }}</div>
        <div class="text-gray-700">{{ getOrder.user.email }}</div>
    </div>
    <div class="flex justify-between mb-6">
        <h1 class="text-lg font-bold"> Metode Pengiriman :</h1>
        <div class="text-gray-700">
            <div>{{ getOrder.orders[0].delivery_type }}</div>
        </div>
    </div>
    <div class="flex justify-between mb-6">
        <h1 class="text-lg font-bold">Metode Pembayaran :</h1>
        <div class="text-gray-700">
            <div>{{ getOrder.orders[0].payment_type }}</div>
        </div>
    </div>
    <table class="w-full mb-8">
        <thead>
            <tr>
                <th class="text-left font-bold text-gray-700">Keterangan</th>
                <th class="text-right font-bold text-gray-700">Jumlah</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="(order, index) in getOrder.orders[0].products.data">
                <td class="text-left text-gray-700">{{ order.name }}</td>
                <td class="text-right text-gray-700">Rp.{{ getOrder.orders[0].grand_total }}</td>
            </tr>
        </tbody>
        <tfoot>
            <tr>
                <td class="text-left font-bold text-gray-700">Total</td>
                <td class="text-right font-bold text-gray-700">Rp.{{ getOrder.orders[0].grand_total }}</td>
            </tr>
        </tfoot>
    </table>
    <div class="text-gray-700 mb-2">Terima kasih atas bisnis Anda!</div>
</div>
<br>
<br>
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