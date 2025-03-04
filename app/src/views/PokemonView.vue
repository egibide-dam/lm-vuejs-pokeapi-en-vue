<script setup>
import { onBeforeMount, reactive, ref, watch } from "vue";

const api_url = 'https://pokeapi.co/api/v2/';
const api_endpoint = 'pokemon';

const id = ref(25);

const pokemon = reactive({
    id: -1,
    nombre: 'Test',
});

// let pokemon_id = document.getElementById('pokemon_id');
// let pokemon_name = document.getElementById('pokemon_name');
// let pokemon_data = document.getElementById('pokemon_data');
// let alert = document.getElementById('error');

function cargarDatos() {
    fetch(api_url + api_endpoint + '/' + id.value)
        .then(response => response.json())
        .then(datos => {
            pokemon.id = id;
            pokemon.nombre = datos.name;

            // pokemon_data.replaceChildren();
            // pokemon_data.append(filaTabla('Experiencia', pokemon.base_experience));
            // pokemon_data.append(filaTabla('Altura', pokemon.height / 10 + ' m'));
            // pokemon_data.append(filaTabla('Peso', pokemon.weight / 10 + ' kg'));
            // pokemon_data.append(filaTabla('Imagen', '<img class="artwork" alt="Artwork oficial" src="' + pokemon.sprites.other['official-artwork'].front_default + '"/>'));
            //
            // alert.classList.add('d-none');
        })
        .catch(error => {
            // pokemon_id.textContent = '?';
            // pokemon_name.textContent = 'Error';
            //
            // alert.textContent = error;
            // alert.classList.remove('d-none');
        });
}

function filaTabla(titulo, contenido) {
    let tr = document.createElement('tr');

    let th = document.createElement('th');
    th.classList.add("table-dark");
    th.textContent = titulo;
    tr.append(th);

    let td = document.createElement('td');
    td.innerHTML = contenido;
    tr.append(td);

    return tr;
}

const boton_menos = () => {
    id.value--;
};

const boton_mas = () => {
    id.value++;
};

onBeforeMount(() => cargarDatos());

watch(id, () => {
    cargarDatos();
})

</script>

<template>
    <div class="col-12 col-sm-6 d-flex justify-content-end align-items-center">
        <span class="me-2">ポケモン ID:</span>
        <button title="Anterior"
                id="boton_menos"
                @click="boton_menos"
                class="btn btn-sm btn-primary">
            <i class="bi bi-dash-lg"></i>
        </button>
        <span class="mx-2">{{ pokemon.id }}</span>
        <button title="Siguiente"
                id="boton_mas"
                @click="boton_mas"
                class="btn btn-sm btn-primary">
            <i class="bi bi-plus-lg"></i>
        </button>
    </div>

    <h2 class="display-2 text-capitalize">{{ pokemon.nombre }}</h2>
    <div class="table-responsive mt-4">
        <table class="table table-hover border">
            <tbody id="pokemon_data" class="align-middle">
            </tbody>
        </table>
    </div>
    <p id="error" class="d-none alert alert-danger" role="alert"></p>
</template>

<style scoped>

</style>
