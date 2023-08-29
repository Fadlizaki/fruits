<template>
  <!-- Main navigation container -->
  <div class="fixed top-0 z-10 bg-gray-50 w-full">
    <nav class="bg-white drop-shadow shadow-red-600">
      <div class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8">
        <div class="relative flex h-16 items-center justify-between">
          <div class="absolute inset-y-0 left-0 flex items-center sm:hidden">
            <!-- Mobile menu button-->
            <div @click="showMenu = !showMenu" class="flex md:hidden">
            <button
              type="button"
              class="
                text-gray-800
                hover:text-gray-400
                focus:outline-none focus:text-gray-400
              "
            >
              <svg viewBox="0 0 24 24" class="w-6 h-6 fill-current">
                <path
                  fill-rule="evenodd"
                  d="M4 5h16a1 1 0 0 1 0 2H4a1 1 0 1 1 0-2zm0 6h16a1 1 0 0 1 0 2H4a1 1 0 0 1 0-2zm0 6h16a1 1 0 0 1 0 2H4a1 1 0 0 1 0-2z"
                ></path>
              </svg>
            </button>
          </div>
            
          </div>
          <div class="flex flex-1 items-center justify-center sm:items-stretch sm:justify-start">
            <div class="flex flex-shrink-0 items-center">
              <span class="self-center text-2xl font-semibold whitespace-nowrap text-red-600">F-fruits</span>
            </div>
            <div class="hidden sm:ml-6 sm:block">
              <div class="flex space-x-4">
                <!-- Current: "bg-gray-900 text-white", Default: "text-gray-300 hover:bg-gray-700 hover:text-white" -->
                <a href="/" class="text-grey-600 hover:text-red-600 rounded-md px-3 py-2 text-sm font-medium">Home</a>
                <a href="/produk"
                  class="text-grey-600 hover:text-red-600 rounded-md px-3 py-2 text-sm font-medium">Product</a>
                <a href="/category"
                  class="text-grey-600 hover:text-red-600 rounded-md px-3 py-2 text-sm font-medium">Category</a>
                <a href="/profil"
                  class="text-grey-600 hover:text-red-600 rounded-md px-3 py-2 text-sm font-medium">Profil</a>
              </div>
            </div>
          </div>
          <div class="absolute inset-y-0 right-0 flex items-center pr-2 sm:static sm:inset-auto sm:ml-6 sm:pr-0">
            <div v-if="isAuthenticated">
              <Keranjang />
            </div>


            <!-- Profile dropdown -->
            <div class="relative ml-3">
              <div v-if="isAuthenticated">
                <div>
                  <a @click="logout"
                    class="text-gray-900 bg-red border border-red-300 focus:outline-none hover:bg-red-100 focus:ring-4 focus:ring-red-200 font-medium rounded-full text-sm px-4 py-2 mr-1 mb-1 dark:bg-red-800 dark:text-white dark:border-red-600 dark:hover:bg-red-700 dark:hover:border-red-600 dark:focus:ring-red-700">Logout</a>
                </div>

              </div>
              <div v-else>
                <a href="/login"
                  class="text-blue-900 bg-white border border-blue-300 focus:outline-none hover:bg-blue-100 focus:ring-4 focus:ring-blue-200 font-medium rounded-full text-sm px-4 py-2 mr-1 mb- dark:bg-blue-800 dark:text-white dark:border-blue-600 dark:hover:bg-blue-700 dark:hover:border-blue-600 dark:focus:ring-blue-700">Login</a>
              </div>
            </div>

            <!--
            Dropdown menu, show/hide based on menu state.

            Entering: "transition ease-out duration-100"
              From: "transform opacity-0 scale-95"
              To: "transform opacity-100 scale-100"
            Leaving: "transition ease-in duration-75"
              From: "transform opacity-100 scale-100"
              To: "transform opacity-0 scale-95"
          -->

          </div>
        </div>
      </div>

      <!-- Mobile menu, show/hide based on menu state. -->
      <div :class="showMenu ? 'flex' : 'hidden'">
        <div class="space-y-1 px-2 pb-3 pt-2">
          <!-- Current: "bg-gray-900 text-white", Default: "text-gray-300 hover:bg-gray-700 hover:text-white" -->
          <a href="/"
            class="block py-2 pl-3 pr-4 text-gray-900 rounded hover:bg-gray-100 md:hover:bg-transparent md:border-0 md:hover:text-red-600 md:p-0 md:hover:text-red-600 hover:text-red-600 md:dark:hover:bg-transparent text-base font-medium">Home</a>
          <a href="/produk"
            class="block py-2 pl-3 pr-4 text-gray-900 rounded hover:bg-gray-100 md:hover:bg-transparent md:border-0 md:hover:text-red-600 md:p-0 md:hover:text-red-600 hover:text-red-600 md:dark:hover:bg-transparent text-base font-medium">Product</a>
          <a href="/category"
            class="block py-2 pl-3 pr-4 text-gray-900 rounded hover:bg-gray-100 md:hover:bg-transparent md:border-0 md:hover:text-red-600 md:p-0 md:hover:text-red-600 hover:text-red-600 md:dark:hover:bg-transparent text-base font-medium">Category</a>
          <a href="/profil"
            class="block py-2 pl-3 pr-4 text-gray-900 rounded hover:bg-gray-100 md:hover:bg-transparent md:border-0 md:hover:text-red-600 md:p-0 md:hover:text-red-600 hover:text-red-600 md:dark:hover:bg-transparent text-base font-medium">Profil</a>

        </div>
      </div>
    </nav>
  </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex';
import Keranjang from './Keranjang.vue';
export default {
  data() {
    return {
      showMenu: false,
    };
  },
  computed: {
    ...mapGetters('auth', ['isAuthenticated']),
  },
  methods: {
    ...mapActions('auth', ['logout']),
  },
  components: { Keranjang }
};

// Initialization for ES Users
import {
  Collapse,
  Dropdown,
  initTE,
} from "tw-elements";

initTE({ Collapse, Dropdown });


</script>



