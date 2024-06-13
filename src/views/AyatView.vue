<template>
    <div v-if="surah">
        <h2>{{ surah.nama }}</h2>
        <ul>
            <li v-for="ayat in ayats" :key="ayat.nomor">
                <div>{{ ayat.nomorAyat }}. {{ ayat.teksArab }}</div>
                <div>{{ ayat.teksLatin }}</div>
                <div>{{ ayat.teksIndonesia }}</div>
            </li>
        </ul>
    </div>
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
