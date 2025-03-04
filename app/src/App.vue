<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
    <div class="row p-4 text-bg-secondary">
        <h1 class="col-12 col-sm-6">Ejemplo PokéAPI</h1>
    </div>

    <main class="p-4">
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/pokemon">Pokemon</RouterLink>
        <RouterView/>
    </main>

    <footer class="row footer mt-auto py-4 bg-secondary-subtle">
        <div class="col text-center">
        <span class="text-secondary">
            <i class="bi bi-github me-2"></i>
            <a class="link link-secondary small link-underline-opacity-0 link-underline-opacity-100-hover"
               href="https://github.com/egibide-dam/pokeapi-fetch">Código fuente disponible en GitHub.</a>
        </span>
        </div>
    </footer>
</template>

<style scoped>
</style>
