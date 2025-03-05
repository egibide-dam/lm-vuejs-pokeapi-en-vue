<script setup>
import { onBeforeMount, reactive, ref, watch } from "vue";
import axios from "axios";

const api_url = 'https://pokeapi.co/api/v2/';
const api_endpoint = 'pokemon';

const id = ref(25);

const pokemon = reactive({
    id: -1,
    nombre: 'Test',
    caracteristicas: [
        {
            campo: 'Altura', valor: 1.0,
        },
    ],
    imagen: 'https://picsum.photos/200'
});

function cargarDatos() {

    const options = {
        method: 'GET',
        url: api_url + api_endpoint + '/' + id.value
    };

    axios.request(options)
        .then(response => response.data)
        .then(datos => {
            pokemon.id = id;
            pokemon.nombre = datos.name;
            pokemon.caracteristicas.push({
                campo: 'Experiencia',
                valor: datos.base_experience
            });
            pokemon.caracteristicas.push({
                campo: 'Altura',
                valor: datos.height / 10 + ' m'
            });
            pokemon.caracteristicas.push({
                campo: 'Peso',
                valor: datos.weight / 10 + ' kg'
            });
            pokemon.imagen = datos.sprites.other['official-artwork'].front_default
        })
        .catch((error) => {
            console.error(error);
        });
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
    <div class="col-12 col-sm-6">
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
            <tr v-for="(caracteristica, index) of pokemon.caracteristicas" :key="index">
                <th class="table-dark">{{ caracteristica.campo }}</th>
                <td>{{ caracteristica.valor }}</td>
            </tr>
            <tr>
                <th class="table-dark">Imagen</th>
                <td><img class="artwork" alt="Artwork oficial" :src="pokemon.imagen"/></td>
            </tr>
            </tbody>
        </table>
    </div>
    <p id="error" class="d-none alert alert-danger" role="alert"></p>
</template>

<style scoped>
.artwork {
    height: 200px;
}
</style>
