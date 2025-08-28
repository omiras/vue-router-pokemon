<template>
  <div v-if="pokemon" class="pokemon-detail">
    <h2>{{ pokemon.name }}</h2>
    <img :src="pokemon.sprite" :alt="pokemon.name" />
    <div><strong>Tipo:</strong> {{ pokemon.type.join(', ') }}</div>
    <div><strong>Evoluciona de:</strong> {{ pokemon.evolves_from_species ? pokemon.evolves_from_species : 'Ninguno' }}</div>
    <div><strong>ID:</strong> {{ pokemon._id }}</div>
  </div>
  <div>
    <button @click="router.push({name: 'home'})">Volver</button>
  </div>
</template>

<script setup>
import router from '@/router';
import { defineProps } from 'vue';
const props = defineProps({
  pokemon: {
    type: Object,
    required: true
  }
});
</script>

<style scoped>
.pokemon-detail {
    color: #000;
font-weight: bold;
  padding: 24px;
  border-radius: 12px;
  background: #f5f5f5;
  box-shadow: 0 2px 8px rgba(0,0,0,0.08);
  max-width: 320px;
  margin: 0 auto;
  text-align: center;
}
.pokemon-detail img {
  width: 128px;
  height: 128px;
  margin-bottom: 16px;
}
</style>
