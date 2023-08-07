<script setup>
import { RouterLink } from 'vue-router'
import {useCounterStore} from '@/store/counter.js'
import { storeToRefs } from "pinia";

const useCounter = useCounterStore()

const {increment} = useCounter
const{count,double} = storeToRefs(useCounter)

const hoy = new Date();
const opciones = { weekday: 'long', year: 'numeric', month: 'short', day: 'numeric' };

const fechaActual = hoy.toLocaleDateString('es-PE', opciones)
</script>

<template>
  <div class="card text-center bg-dark">
    <div class="card-header">
      Vue Router + Vite + PokeAPI:
      <h2>Home Counter: {{count}}</h2> 
      <h2>Double: {{ double}}</h2>
      <button @click="increment">Increment</button>
      
    </div>
    <div class="card-body">
      <h5 class="card-title">Proyecto desarrollado con Vue3</h5>
      <p class="card-text">Este proyecto ha sido desarrollado con la finalidad de aprender más sobre vue Router v4.</p>
      <router-link class="btn btn-primary" to="/pokemons">Ver Pokemones</router-link>
    </div>
    <div class="card-footer text-muted">
      {{ fechaActual }}
    </div>
  </div>
</template>
