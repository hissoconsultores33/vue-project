<script setup>
import { useFavoritoStore } from '@/store/favoritos'
import { storeToRefs } from 'pinia';
import {RouterLink} from 'vue-router'

const useFavoritos = useFavoritoStore()

const { favoritos} = storeToRefs(useFavoritos)
const {remove} = useFavoritos
</script>

<template>
    <div class="alert alert-primary mt-5 text-center" v-if="favoritos.length === 0"  role="alert">
        No tienes Pokemones favoritos!!!
    </div>
    <div class="row row-cols-auto m-auto justify-content-center" v-else>
        <div class="card mt-5" v-for="pokemon in favoritos" :key="pokemon.id" style="width: 20rem;">
            <img :src="pokemon.sprites?.front_default" class="card-img-top bg-dark" :alt="pokemon.name">
            <div class="card-body">
                <h5 class="card-title text-center text-uppercase">{{ $route.params.name }}<span
                        v-for="(tipo, index) in pokemon.types" :key="index" class="badge bg-info ms-1 me-1">
                        {{ tipo.type.name }}
                    </span></h5>
                <ul class="list-group list-group-flush">
                    <li class="list-group-item">Altura: {{ pokemon.height * 10 }}cm</li>
                    <li class="list-group-item">Peso: {{ pokemon.weight * 0.1 }}kg</li>

                </ul>

            </div>
            <div class="d-flex justify-content-between">
                <router-link :to="`/pokemons/${pokemon.name}`"  class="btn btn-sm btn-outline-primary m-2">Más Información</router-link>
                <button @click="remove(pokemon.id)" class="btn btn-sm btn-outline-danger m-2">Eliminar</button>
            </div>
        </div>
    </div>
</template>