<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <nav class="navbar bg-dark">
    <div class="container">
      <router-link class="navbar-brand text-white" to="/">
        <img src="@/assets/logo.svg" alt="Logo" width="30" height="24" class="d-inline-block align-text-top">
        Pokemon API
      </router-link>
      <div>
        <router-link class="btn btn-outline-primary me-2" to="/">Home</router-link>
        <router-link class="btn btn-outline-primary me-2" to="/pokemons">Pokemons</router-link>
        <router-link class="btn btn-outline-primary" to="/favoritos">Mis Favoritos</router-link>
      </div>
    </div>
  </nav>
  <div class="container">

    <RouterView />
  </div>
</template>
