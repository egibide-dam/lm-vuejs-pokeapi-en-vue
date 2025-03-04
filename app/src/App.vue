<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
    <div class="row p-4 text-bg-secondary">
        <h1 class="col-12 col-sm-6">Ejemplo PokéAPI</h1>
        <div class="col-12 col-sm-6 d-flex justify-content-end align-items-center">
            <span class="me-2">ポケモン ID:</span>
            <button title="Anterior"
                    id="boton_menos"
                    class="btn btn-sm btn-primary">
                <i class="bi bi-dash-lg"></i>
            </button>
            <span id="pokemon_id" class="mx-2"></span>
            <button title="Siguiente"
                    id="boton_mas"
                    class="btn btn-sm btn-primary">
                <i class="bi bi-plus-lg"></i>
            </button>
        </div>
    </div>

    <main class="p-4">
        <RouterLink to="/">Home</RouterLink>

        <h2 id="pokemon_name" class="display-2 text-capitalize"></h2>
        <div class="table-responsive mt-4">
            <table class="table table-hover border">
                <tbody id="pokemon_data" class="align-middle">
                </tbody>
            </table>
        </div>
        <p id="error" class="d-none alert alert-danger" role="alert"></p>
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
