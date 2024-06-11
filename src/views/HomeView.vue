<template>
    <div class="navbar bg-secondary shadow px-20">
        <div class="navbar-start">
            <a class="btn btn-ghost text-xl">Asy-Syifa</a>
        </div>
        <div class="navbar-end">
            <button class="btn btn-ghost btn-circle">
                <i class="bi bi-search text-xl"></i>
            </button>
            <label class="swap swap-rotate btn btn-ghost btn-circle">
                <input type="checkbox" class="theme-controller" value="synthwave" @change="toggleTheme"/>
                <i class="bi bi-sun swap-off text-2xl"></i>
                <i class="bi bi-moon swap-on text-xl"></i>
            </label>
        </div>
    </div>
    <div v-for="quran in qurans" :key="quran.nomor" class="text-primary">
        {{ quran.nama }}
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';

const qurans = ref([])
const isDarkTheme = ref(false)

const toggleTheme = () => {
    isDarkTheme.value = !isDarkTheme.value
    document.documentElement.setAttribute('data-theme', isDarkTheme.value ? 'luxury' : 'nord')
}

onMounted(() => {
    axios
    .get('https://equran.id/api/surat')
    .then(response => {
        qurans.value = response.data;
    })
    .catch(error => {
        console.error('Terjadi kesalahan saat mengambil data:', error);
    });
})
</script>
