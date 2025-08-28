<template>
  <div>
    <div v-if="loading">Loading...</div>
    <div v-else>
      <div v-if="selectedPokemon">
        <PokemonDetail :pokemon="selectedPokemon" />
        <button @click="selectedPokemon = null" style="margin: 16px 0;">Volver</button>
      </div>
      <div v-else class="pokemon-list">
        <div v-for="pokemon in pokemons" :key="pokemon.name" class="pokemon-item" @click="selectPokemon(pokemon)" style="cursor:pointer;">
          <img :src="pokemon.sprite" :alt="pokemon.name" />
          <div>{{ pokemon.name }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import PokemonDetail from './PokemonDetail.vue';

export default {
  name: 'PokemonList',
  components: { PokemonDetail },
  setup() {
    const pokemons = ref([]);
    const loading = ref(true);
    const selectedPokemon = ref(null);

    const selectPokemon = (pokemon) => {
      selectedPokemon.value = pokemon;
    };

    onMounted(async () => {
      try {
        const response = await fetch('https://pokemon-server-3a2p.onrender.com/api/pokemons');
        const data = await response.json();
        pokemons.value = data.slice(0, 20);
      } catch (error) {
        console.error(error);
      } finally {
        loading.value = false;
      }
    });

    return {
      pokemons,
      loading,
      selectedPokemon,
      selectPokemon
    };
  }
};
</script>

<style scoped>
.pokemon-list {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 16px;    
}
.pokemon-item {
    color: #7a7272;
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 120px;
  padding: 8px;
  border: 1px solid #eee;
  border-radius: 8px;
  background: #fafafa;
  font-weight: bold;
}
.pokemon-item img {
  width: 96px;
  height: 96px;
}
</style>
