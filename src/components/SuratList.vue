<template>
    <div class="flex justify-center">
        <input v-model="searchQuery" type="text" placeholder="Search Surah" class="w-full lg:mx-20 mx-5 mt-9 mb-5 text-center py-3 border border-gray-300 rounded-full">
    </div>
    <div class="flex justify-center lg:gap-10 gap-5 text-sm">
        <a href="/surah/36" class="hover:opacity-80">Yasin</a>
        <a href="/surah/66" class="hover:opacity-80">Al-Waqi'ah</a>
        <a href="/surah/67" class="hover:opacity-80">Al-Mulk</a>
        <a href="/surah/18" class="hover:opacity-80">Al-Kahf</a>
        <a href="/surah/55" class="hover:opacity-80">Ar-Rahman</a>
    </div>
    <div class="grid lg:grid-cols-3 md:grid-cols-2 sm:grid-cols-1 gap-4 lg:mx-20 mx-5 my-5">
        <div v-for="surah in filteredQurans" :key="surah.nomor" @click="selectSurah(surah)" class="bg-secondary lg:p-4 p-2 rounded-md cursor-pointer transition duration-200 hover:scale-105 hover:shadow-lg">
            <div class="flex items-center">
                <div class="flex items-center justify-center lg:w-16 w-8 lg:h-14 h-8 lg:text-2xl text-lg bg-primary text-base-300 rounded-full">{{ surah.nomor }}</div>
                <div class="flex-auto lg:w-64 w-32 ml-4">
                    <div class="text-lg font-bold">{{ surah.namaLatin }}</div>
                    <div class="text-xs">{{ surah.arti }} - {{ surah.jumlahAyat }} Ayat</div>
                </div>
                <div class="flex-auto w-24 text-xl text-right">{{ surah.nama }}</div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import { defineProps, defineEmits } from 'vue';

const props = defineProps({
    qurans: Array,
})

const emit = defineEmits(['selectSurah']);

const searchQuery = ref('');

const filteredQurans = computed(() => {
    return props.qurans.filter(surah => 
        surah.namaLatin.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
        surah.arti.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
        surah.nama.toLowerCase().includes(searchQuery.value.toLowerCase())
    );
});

const selectSurah = (surah) => {
    emit('selectSurah', surah);
}
</script>