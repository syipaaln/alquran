<template>
  <div>
    <div class="navbar bg-secondary shadow px-20">
        <div class="navbar-start">
            <a class="btn btn-ghost text-xl">Asy-Syifa</a>
        </div>
        <div class="navbar-end">
            <label class="swap swap-rotate btn btn-ghost btn-circle">
                <input type="checkbox" class="theme-controller" @change="toggleTheme"/>
                <i class="bi bi-sun swap-off text-2xl"></i>
                <i class="bi bi-moon swap-on text-xl"></i>
            </label>
        </div>
    </div>
    <RouterView />
  </div>
</template>

<script setup>
import { ref } from 'vue'
const isDarkTheme = ref(false)

const toggleTheme = () => {
    isDarkTheme.value = !isDarkTheme.value
    document.documentElement.setAttribute('data-theme', isDarkTheme.value ? 'luxury' : 'nord')
}

</script>