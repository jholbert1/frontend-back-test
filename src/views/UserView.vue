<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import { useRouter } from 'vue-router';
import { useToast } from "vue-toastification";

const toast = useToast();
const router = useRouter();

const userData = ref({
    firstName: '',
    lastName: '',
    username: '',
    email: '',
    id: ''
});

onMounted(async () => {
    try {
        const token = localStorage.getItem("token");

        if (!token) {
            router.push('/');
            return
        };

        const { data } = await axios.get(`http://localhost:3000/api/auth/profile`, {
            headers: {
                Authorization: `Bearer ${token}`
            }
        });

        userData.value = data.data;
    } catch (error) {
        toast.error(`Parece que hubo un error registrando al usuario, ${error.response.data.message}`)
    }
});

const editUserData = async () => {
    try {
        const token = localStorage.getItem("token");
        const { data } = await axios.patch(`http://localhost:3000/api/user/${userData.value.id}`,
            {
                firstName: userData.value.firstName,
                lastName: userData.value.lastName,
                username: userData.value.username,
                email: userData.value.email,
            }, {
            headers: {
                Authorization: `Bearer ${token}`
            }
        });

        userData.value = data.data;
        toast.info("Has actualizado tus datos con exitos!");
    } catch (error) {
        toast.error(`Parece que hubo un error registrando al usuario, ${error.response.data.message}`)
    }
};

const closeSession = async () => {
    try {
        const token = localStorage.getItem("token");
        await axios.get(`http://localhost:3000/api/auth/logout`, {
            headers: {
                Authorization: `Bearer ${token}`
            }
        });
        toast("Hasta Luego");
        localStorage.removeItem("token");
        router.push('/');
    } catch (error) {
        toast.error(`Parece que hubo un error saliendo, ${error.response.data.message}`)
    }
};
</script>

<template>
    <div class="bg-black min-h-screen flex justify-center items-center">
        <div class="bg-purple-500 p-8 rounded-md w-96">

            <h2 class="text-center text-white text-lg mb-5">Datos del usuario</h2>
            <div class="pl-4">
                <div class="mb-4">
                    <label class="block text-white mb-2">First Name:</label>
                    <input v-model="userData.firstName" class="p-2 w-full rounded-md" />

                </div>
                <div class="mb-4">
                    <label class="block text-white mb-2">Last Name:</label>
                    <input v-model="userData.lastName" class="p-2 w-full rounded-md" />
                </div>
                <div class="mb-4">
                    <label class="block text-white mb-2">Username:</label>
                    <input v-model="userData.username" class="p-2 w-full rounded-md" />
                </div>
                <div class="mb-4">
                    <label class="block text-white mb-2">Email:</label>
                    <input v-model="userData.email" class="p-2 w-full rounded-md" />
                </div>
                <button class="block w-full bg-purple-700 p-2 rounded-md text-white mb-4 hover:bg-purple-600"
                    @click.prevent="editUserData">
                    Edit
                </button>
                <button className="block w-full bg-purple-700 p-2 rounded-md text-white text-center hover:bg-purple-600"
                    @click.prevent="closeSession">Go Out
                </button>
            </div>
        </div>
    </div>
</template>

<style></style>
