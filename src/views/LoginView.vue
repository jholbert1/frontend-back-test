<script setup>
import axios from 'axios';
import { ref } from 'vue';
import { RouterLink, useRouter } from 'vue-router';
import { useToast } from "vue-toastification";

const router = useRouter();
const toast = useToast();

const userNameOrEmail = ref('');
const password = ref('');

const submitForm = async () => {
  try {
    const { data } = await axios.post('http://localhost:3000/api/auth/login', {
      userNameOrEmail: userNameOrEmail.value,
      password: password.value,
    });
    const token =  data.data.access_token;
    localStorage.setItem("token", token);
    toast("Bienvenido");
    router.push('/user');
  } catch (error) {
    toast.error(`${error.response.data.message}`)
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
          <input v-model="userNameOrEmail" className="p-2 w-full rounded-md" type="text" id="userNameOrEmail"
            name="userNameOrEmail" />
        </div>
        <div className="mb-4">
          <label className="block text-white mb-2" htmlFor="lastName">
            Last Name
          </label>
          <input v-model="password" className="p-2 w-full rounded-md" type="password" id="password" name="password" />
        </div>
        <button className="block w-full bg-purple-700 p-2 rounded-md text-white mb-4 hover:bg-purple-600">
          Login
        </button>
        <RouterLink className="block w-full bg-purple-700 p-2 rounded-md text-white text-center hover:bg-purple-600"
          to="/">Register
        </RouterLink>
      </form>
    </div>
  </div>
</template>

<style></style>
