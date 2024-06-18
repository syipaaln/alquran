<template>
    <div class="text-2xl text-center mt-5">{{ surah.nama }}</div>
    <div class="text-xl text-center font-bold">{{ surah.namaLatin }}</div>
    <div class="flex justify-center items-center">
        <div class="text-sm">{{ surah.tempatTurun }}</div>
        <div class="text-md font-medium mx-5">{{ surah.arti }}</div>
        <div class="text-sm">{{ surah.jumlahAyat }} Ayat</div>
    </div>
    <div class="flex justify-between mx-36">
        <a href="/" class="btn btn-accent rounded-full">
            <i class="bi bi-arrow-return-left text-xl"></i>
            <span>Kembali</span>
        </a>
        <button @click="playAudio(surah.audioFull['05'])" class="btn btn-accent rounded-full">
            <i :class="{'bi bi-play-circle': !isPlaying, 'bi bi-pause-circle': isPlaying}" class="text-xl"></i>
            <span>Putar Murottal</span>
        </button>
    </div>
    <ul class="px-36">
        <li v-for="ayat in ayats" :key="ayat.nomor" class="my-10 border-b border-neutral-content">
            <div class="flex justify-between items-center">
                <div class="">{{ ayat.nomorAyat }}.</div>
                <div class="text-2xl">{{ ayat.teksArab }}</div>
            </div>
            <div class="flex items-center">
                <button @click="playAudio(ayat.audio['05'])" class="btn btn-circle">
                    <i :class="{'bi bi-play-circle': !isPlaying, 'bi bi-pause-circle': isPlaying}" class="text-xl"></i>
                </button>
                <div class="ml-3 text-lg font-medium">{{ ayat.teksLatin }}</div>
            </div>
            <div class="ml-10 mt-2 text-sm">{{ ayat.teksIndonesia }}</div>
        </li>
    </ul>
    <audio ref="audioPlayer" class="hidden" controls>
        <!-- <source :src="audioUrl" type="audio/mp3"> -->
        Your browser does not support the audio element.
    </audio>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRoute } from 'vue-router';
import axios from 'axios';

const route = useRoute();
const surah = ref({});
const ayats = ref([]);
const audioPlayer = ref(null);
const isPlaying = ref(false);


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

const playAudio = (audioUrl) => {
    if (!audioPlayer.value) {
        audioPlayer.value.src = audioUrl;
        // audioPlayer.value.play().catch(error => {
        //     console.error('Gagal memutar audio:', error);
        // });
    }
    if (isPlaying.value) {
        audioPlayer.value.pause();
    } else {
        audioPlayer.value.play();
    }
    isPlaying.value = !isPlaying.value;
};
</script>
