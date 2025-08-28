<template>
  <div>
    <PokemonDetail :pokemon="pokemon" v-if="pokemon" />
    <div v-else>Cargando...</div>
    <button @click="goBack" style="margin: 16px 0;">Volver</button>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRoute, useRouter } from 'vue-router';
import PokemonDetail from '../components/PokemonDetail.vue';

const route = useRoute();
const router = useRouter();
const pokemon = ref(null);

const goBack = () => {
  router.back();
};

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
