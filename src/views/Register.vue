<template>
    <div class="min-h-screen bg-gray-50 flex flex-col justify-center py-12 sm:px-6 lg:px-8">
        <div class="sm:mx-auto sm:w-full sm:max-w-md">
            <img class="mx-auto h-10 w-auto" src="https://www.svgrepo.com/show/301692/login.svg" alt="Workflow">
            <h2 class="mt-6 text-center text-3xl leading-9 font-extrabold text-gray-900">
                Membuat akun baru
            </h2>
            <p class="mt-2 text-center text-sm leading-5 text-gray-500 max-w">
                Or
                <a href="#"
                    class="font-medium text-blue-600 hover:text-blue-500 focus:outline-none focus:underline transition ease-in-out duration-150">
                    Atau login ke akun Anda
                </a>
            </p>
        </div>

        <div class="mt-8 sm:mx-auto sm:w-full sm:max-w-md">
            <div class="bg-white py-8 px-4 shadow sm:rounded-lg sm:px-10">
                <h3 class="text-2xl font-bold text-center">Daftar</h3>
                <form action="" @submit.prevent="performRegister">
                    <div class="mt-4">
                        <div>
                            <label class="block" for="Name">Username</label>
                            <input type="text" placeholder="Name" v-model="name"
                                class="w-full px-4 py-2 mt-2 border rounded-md focus:outline-none focus:ring-1 focus:ring-blue-600">
                        </div>
                        <div class="mt-4">
                            <label class="block" for="email">Email</label>
                            <input type="text" placeholder="Email" v-model="email"
                                class="w-full px-4 py-2 mt-2 border rounded-md focus:outline-none focus:ring-1 focus:ring-blue-600">
                        </div>
                        <div class="mt-4">
                            <label class="block" for="email">Phone</label>
                            <input type="number" placeholder="Phone" v-model="phone"
                                class="w-full px-4 py-2 mt-2 border rounded-md focus:outline-none focus:ring-1 focus:ring-blue-600">
                        </div>
                        <div class="mt-4">
                            <label class="block">Password</label>
                            <input type="password" placeholder="Password" v-model="password"
                                class="w-full px-4 py-2 mt-2 border rounded-md focus:outline-none focus:ring-1 focus:ring-blue-600">
                        </div>
                        <div class="mt-4">
                            <label class="block">Confirm_Password</label>
                            <input type="password" placeholder="Password" v-model="confirm_password"
                                class="w-full px-4 py-2 mt-2 border rounded-md focus:outline-none focus:ring-1 focus:ring-blue-600">
                        </div>

                        <div class="flex">
                            <button class="w-full px-6 py-2 mt-4 text-white bg-blue-600 rounded-lg hover:bg-blue-900">Create
                                Account</button>
                        </div>
                        <div class="mt-6 text-grey-dark">
                            Sudah Punya Akun?
                            <a class="text-blue-600 hover:underline" href="/login">
                                Log in
                            </a>
                        </div>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>

  

<script>
import { mapActions } from 'vuex';

export default {
    data() {
        return {
            name: '',
            email: '',
            phone: '',
            password: '',
            confirm_password: ''
        };
    },
    methods: {
        ...mapActions('auth', ['register']),
        async performRegister() {
            const dataUser = {
                name: this.name,
                email: this.email,
                phone: this.phone,
                password: this.password,
                confirm_password: this.confirm_password
            };

            const success = await this.register(dataUser);

            if (success) {
                // Redirect to the desired route on successful login
                this.$router.push('/login');
            } else {
                alert("Register Gagal");
            }
        },
    },
};
</script>