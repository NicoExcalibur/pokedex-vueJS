<template>
    <div class="container">
        <h1>Pokedex</h1>
        <PokemonList 
            :imageUrl="imageUrl" 
            :apiUrl="apiUrl" 
            @setPokemonUrl="setPokemonUrl" />
    </div>
</template>

<script>
import PokemonList from './PokemonList.vue';

export default {
  
    data: () => {
        return {
        imageUrl: 'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/',
        apiUrl: 'https://pokeapi.co/api/v2/pokemon/'
        }
    },
    components: { 
        PokemonList 
    },
}

</script>

<style lang="sass">

</style>