<script setup>
import { RouterView } from 'vue-router'
import BarraNavegacion from "@/components/BarraNavegacion.vue";
</script>

<template>
    <BarraNavegacion/>

    <main class="p-4">
        <RouterView/>
    </main>

    <footer class="row footer mt-auto py-4 bg-secondary-subtle">
        <div class="col text-center">
        <span class="text-secondary">
            <i class="bi bi-github me-2"></i>
            <a class="link link-secondary small link-underline-opacity-0 link-underline-opacity-100-hover"
               target="_blank"
               href="https://github.com/egibide-dam/lm-vuejs-pokeapi-en-vue">Código fuente disponible en GitHub.</a>
        </span>
        </div>
    </footer>
</template>

