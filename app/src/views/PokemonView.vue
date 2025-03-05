<script setup>
import { onBeforeMount, reactive, ref, watch } from "vue";
import axios from "axios";

const api_url = 'https://pokeapi.co/api/v2/';
const api_endpoint = 'pokemon';

const id = ref(1025);

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

    pokemon.caracteristicas = [];

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
    if (id.value > 1)
        id.value--;
};

const boton_mas = () => {
    if (id.value < 1025)
        id.value++;
};

onBeforeMount(() => cargarDatos());

watch(id, () => {
    cargarDatos();
})

</script>

<template>
    <div class="row">
        <div class=" col-12 col-md-3">
            <div class="card">
                <div class="card-header">
                    <span class="me-2">ポケモン ID</span>
                </div>
                <div class="card-body d-flex justify-content-between align-items-center flex-md-wrap">
                    <button title="Anterior"
                            @click="boton_menos"
                            class="btn btn-primary">
                        <i class="bi bi-dash-lg"></i>
                    </button>
                    <span class="fs-2 mx-2">{{ pokemon.id }}</span>
                    <button title="Siguiente"
                            @click="boton_mas"
                            class="btn btn-primary">
                        <i class="bi bi-plus-lg"></i>
                    </button>
                </div>
            </div>
        </div>
        <div class="col-12 col-md-9 ps-md-3 pt-3 pt-md-0">
            <h2 class="display-2 text-capitalize">{{ pokemon.nombre }}</h2>
            <div class="table-responsive">
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
        </div>
    </div>
</template>

<style scoped>
.artwork {
    height: 200px;
}
</style>
