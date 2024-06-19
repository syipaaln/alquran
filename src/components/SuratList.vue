<template>
    <!-- <input v-model="searchQuery" type="text" placeholder="Search Surah" class="mb-5 p-2 border border-gray-300 rounded"> -->
    <div class="grid grid-cols-3 gap-4 mx-20 my-5">
        <div v-for="surah in filteredQurans" :key="surah.nomor" @click="selectSurah(surah)" class="bg-secondary p-4 rounded-md cursor-pointer transition duration-200 hover:scale-105 hover:shadow-lg">
            <div class="flex items-center">
                <div class="flex-none w-14 text-2xl bg-primary text-base-300 rounded-full h-14 flex items-center justify-center">{{ surah.nomor }}</div>
                <div class="flex-auto w-64 ml-4">
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
    searchQuery: String
})

const emit = defineEmits(['selectSurah']);

// const searchQuery = ref('');

const filteredQurans = computed(() => {
    return props.qurans.filter(surah => 
        surah.namaLatin.toLowerCase().includes(props.searchQuery.toLowerCase()) ||
        surah.arti.toLowerCase().includes(props.searchQuery.toLowerCase()) ||
        surah.nama.toLowerCase().includes(props.searchQuery.toLowerCase())
    )
})

const selectSurah = (surah) => {
    emit('selectSurah', surah);
}
</script>