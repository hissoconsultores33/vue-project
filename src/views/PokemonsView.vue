<script setup>

import { RouterLink } from 'vue-router';
import { useGetData } from '@/composables/getData'

const { data, getData, loading, error } = useGetData();

getData('https://pokeapi.co/api/v2/pokemon')

</script>

<template>
    <p class="mt-5" v-if="loading">Cargando información...</p>

    <div class="alert alert-danger text-center mt-5" v-if="error">{{ error }}</div>
    <div v-if="data">
        <ul class="bg-dark mt-2 rounded shadow-lg list-group">
            <li class="list-group-item list-group-item-action" v-for="pokemon in data.results">
                <router-link :to="`/pokemons/${pokemon.name}`">
                    {{ pokemon.name }}
                </router-link>
            </li>
        </ul>
        <div class="btn-group mt-2 float-end">
            <button :disabled="!data.previous" class="btn btn-sm btn-success me-2"
                @click="getData(data.previous)">Anterior</button>
            <button :disabled="!data.next" class="btn btn-sm btn-primary" @click="getData(data.next)">Siguiente</button>
        </div>
    </div>

</template>