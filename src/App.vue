<template>
  <div>
    <div class="navbar bg-secondary shadow px-20">
        <div class="navbar-start">
            <a class="btn btn-ghost text-xl">Asy-Syifa</a>
        </div>
        <div class="navbar-center">
            <input v-if="showSearch" v-model="searchQuery" type="text" placeholder="Search Surah" class="input input-bordered"/>
        </div>
        <div class="navbar-end">
            <button @click="toggleSearch" class="btn btn-ghost btn-circle">
                <i class="bi bi-search text-xl"></i>
            </button>
            <label class="swap swap-rotate btn btn-ghost btn-circle">
                <input type="checkbox" class="theme-controller" @change="toggleTheme"/>
                <i class="bi bi-sun swap-off text-2xl"></i>
                <i class="bi bi-moon swap-on text-xl"></i>
            </label>
        </div>
    </div>
    <RouterView :searchQuery="searchQuery" />
  </div>
</template>

<script setup>
import { ref } from 'vue'
const isDarkTheme = ref(false)
const showSearch = ref(false)
const searchQuery = ref('')

const toggleTheme = () => {
    isDarkTheme.value = !isDarkTheme.value
    document.documentElement.setAttribute('data-theme', isDarkTheme.value ? 'luxury' : 'nord')
}

const toggleSearch = () => {
    showSearch.value = !showSearch.value
}
</script>