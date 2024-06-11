<template>
    <div class="grid grid-cols-3 gap-4 mx-20 my-5">
        <div v-for="quran in qurans" :key="quran.nomor" class="bg-secondary p-4 rounded-md cursor-pointer transition duration-200 hover:scale-105 hover:shadow-lg">
            <div class="flex items-center">
                <div class="flex-none w-14 text-2xl bg-primary text-base-300 rounded-full h-14 flex items-center justify-center">{{ quran.nomor }}</div>
                <div class="flex-auto w-64 ml-4">
                    <div class="text-lg font-bold">{{ quran.nama_latin }}</div>
                    <div class="text-xs">{{ quran.arti }} - {{ quran.jumlah_ayat }} Ayat</div>
                </div>
                <div class="flex-auto w-24 text-xl text-right">{{ quran.nama }}</div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    qurans: Array
})
</script>