<template>
    <div class="text-2xl text-center mt-5">{{ surah.nama }}</div>
    <div class="text-xl text-center font-bold">{{ surah.namaLatin }}</div>
    <div class="flex justify-center items-center">
        <div class="text-sm">{{ surah.tempatTurun }}</div>
        <div class="text-md font-medium mx-5">{{ surah.arti }}</div>
        <div class="text-sm">{{ surah.jumlahAyat }} Ayat</div>
    </div>
    <ul class="px-36">
        <li v-for="ayat in ayats" :key="ayat.nomor" class="my-10 border-b border-neutral-content">
            <div class="flex justify-between items-center">
                <div class="">{{ ayat.nomorAyat }}.</div>
                <div class="text-2xl">{{ ayat.teksArab }}</div>
            </div>
            <div class="ml-10 my-5">
                <div class="text-lg font-medium">{{ ayat.teksLatin }}</div>
                <div>{{ ayat.teksIndonesia }}</div>
            </div>
        </li>
    </ul>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRoute } from 'vue-router';
import axios from 'axios';

const route = useRoute();
const surah = ref({});
const ayats = ref([]);

onMounted(() => {
    const surahNumber = route.params.id;
    axios
        .get(`https://equran.id/api/v2/surat/${surahNumber}`)
        .then(response => {
            surah.value = response.data.data;
            ayats.value = response.data.data.ayat;
        })
        .catch(error => {
            console.error('Terjadi kesalahan saat mengambil data:', error);
        });
});
</script>
