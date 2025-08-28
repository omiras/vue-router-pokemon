<template>
  <div>
    <PokemonDetail :pokemon="pokemon" v-if="pokemon" />
    <div v-else>Cargando...</div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRoute } from 'vue-router';
import PokemonDetail from '../components/PokemonDetail.vue';

const route = useRoute();
const pokemon = ref(null);

onMounted(async () => {
  try {
    const response = await fetch('https://pokemon-server-3a2p.onrender.com/api/pokemons/' + route.params.id);
    const data = await response.json();
    pokemon.value = data;
  } catch (error) {
    console.error(error);
  }
});
</script>
