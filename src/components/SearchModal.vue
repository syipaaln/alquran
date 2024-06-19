<template>
    <div>
        <input v-model="searchQuery" type="text" placeholder="Search Surah" class="mb-5 p-2 border border-gray-300 rounded">
    </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const searchQuery = ref('');

const filteredQurans = computed(() => {
    return props.qurans.filter(surah => 
        surah.namaLatin.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
        surah.arti.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
        surah.nama.toLowerCase().includes(searchQuery.value.toLowerCase())
    );
});
</script>