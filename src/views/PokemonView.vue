<script setup>
import { useRoute, useRouter } from 'vue-router'
import { useGetData } from '@/composables/getData'
import { useFavoritoStore } from '@/store/favoritos'


const route = useRoute()
const router = useRouter()
const useFavoritos = useFavoritoStore()

const { add, findPokemon } = useFavoritos

const back = () => {
    router.push('/pokemons')
}

const { data, getData, loading, error } = useGetData();

getData(`https://pokeapi.co/api/v2/pokemon/${route.params.name}`);

</script>
<template>
    <p class="mt-5" v-if="loading">Cargando información...</p>
    <div class="alert alert-danger mt-5 text-center" v-if="error">{{ error }}</div>
    <div class="d-flex justify-content-center" v-if="data">
        <div class="card mt-5" style="width: 20rem;">
            <img :src="data.sprites?.front_default" class="card-img-top bg-dark" :alt="data.name">
            <div class="card-body">
                <h5 class="card-title text-center text-uppercase">{{ $route.params.name }}<span
                        v-for="(tipo, index) in data.types" :key="index" class="badge bg-info ms-1 me-1">
                        {{ tipo.type.name }}
                    </span></h5>
                <ul class="list-group list-group-flush">
                    <li class="list-group-item">Altura: {{ data.height * 10 }}cm</li>
                    <li class="list-group-item">Peso: {{ data.weight * 0.1 }}kg</li>

                </ul>
                <button :disabled="findPokemon(data.name)" class="btn btn-primary mt-2" @click="add(data)">Agregar Favoritos</button>
            </div>
        </div>
    </div>
    <button class="btn btn-outline-primary mt-2 " @click="back">Regresar</button>

    <!-- <div class="position-relative" v-else>
        <div class="position-absolute top-0 start-50 translate-middle-x">
            <h2 class="bg-dark text-white text-center mt-5 rounded shadow-lg">Tu pokédex no ha encontrado este pokemon
            </h2>
            <button class="btn btn-outline-primary mt-2 text-center" @click="back">Regresar</button>
        </div>
    </div> -->

</template>