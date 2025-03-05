<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
    <nav class="row navbar navbar-expand p-4 text-bg-secondary">
        <div class="container-fluid">
            <h1>
                <RouterLink class="nav-link text-bg-secondary" :to="{ name: 'home' }">Ejemplo PokéAPI</RouterLink>
            </h1>
            <div class="collapse navbar-collapse">
                <ul class="navbar-nav m-0 align-items-center ms-auto">
                    <li class="nav-item">
                        <RouterLink class="nav-link text-bg-secondary" :to="{ name: 'home' }">Home</RouterLink>
                    </li>
                    <li class="nav-item mx-2">|</li>
                    <li class="nav-item">
                        <RouterLink class="nav-link text-bg-secondary" :to="{ name: 'pokemon' }">Pokemon</RouterLink>
                    </li>
                </ul>
            </div>
        </div>
    </nav>

    <main class="p-4">
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
