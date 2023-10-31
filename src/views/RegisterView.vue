<script setup>
import axios from 'axios';
import { ref } from 'vue';
import { RouterLink, useRouter } from 'vue-router';

import { useToast } from "vue-toastification";

const router = useRouter();
const toast = useToast();

const firstName = ref('');
const lastName = ref('');
const username = ref('');
const email = ref('');
const password = ref('');

const submitForm = async () => {
  try {
    await axios.post('http://localhost:3000/api/user', {
      firstName: firstName.value,
      lastName: lastName.value,
      username: username.value,
      email: email.value,
      password: password.value
    });
    toast("Usuario creado con exitos!");
    router.push('/login');
  } catch (error) {
    toast.error(`Parece que hubo un error registrando al usuario, ${error.response.data.message}`)
  }
};
</script>

<template>
  <div className="bg-black min-h-screen flex justify-center items-center">
    <div className="bg-purple-500 p-8 rounded-md w-96">
      <form @submit.prevent="submitForm">
        <div className="mb-4">
          <label className="block text-white mb-2" htmlFor="firstName">
            First Name
          </label>
          <input v-model="firstName" className="p-2 w-full rounded-md" type="text" id="firstName" name="firstName" />
        </div>
        <div className="mb-4">
          <label className="block text-white mb-2" htmlFor="lastName">
            Last Name
          </label>
          <input v-model="lastName" className="p-2 w-full rounded-md" type="text" id="lastName" name="lastName" />
        </div>
        <div className="mb-4">
          <label className="block text-white mb-2" htmlFor="username">
            Username
          </label>
          <input v-model="username" className="p-2 w-full rounded-md" type="text" id="username" name="username" />
        </div>
        <div className="mb-4">
          <label className="block text-white mb-2" htmlFor="email">
            Email
          </label>
          <input v-model="email" className="p-2 w-full rounded-md" type="email" id="email" name="email" />
        </div>
        <div className="mb-4">
          <label className="block text-white mb-2" htmlFor="password">
            Password
          </label>
          <input v-model="password" className="p-2 w-full rounded-md" type="password" id="password" name="password" />
        </div>
        <button className="block w-full bg-purple-700 p-2 rounded-md text-white mb-4 hover:bg-purple-600">
          Register
        </button>
        <RouterLink className="block w-full bg-purple-700 p-2 rounded-md text-white text-center hover:bg-purple-600"
          to="/login">Login
        </RouterLink>
      </form>
    </div>
  </div>
</template>
