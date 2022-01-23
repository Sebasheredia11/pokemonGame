<template>

  <div class="pokemon-container">
    <img class="hidden-pokemon" :src="imgSrc" alt="pokemon">
    <img v-if="showPokemon" 
    class="fade-in" 
    :src="imgSrc" 
    alt="pokemon">
  </div>

</template>

<script>


export default {
  name: 'PokemonPicture',
  props: {
    pokemonId: {
      type: Number,
      required: true
    },
    showPokemon:{
      type: Boolean,
      required: true,
      default: false
    }
  },
  computed: {
    imgSrc() {
      return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.pokemonId}.svg`
    }
  },
}
</script>

<style scoped>
  .pokemon-container {
    height: 200px;
    justify-content: center;
    flex: 0%;
  }
  img {
      height: 200px;
      margin-left:auto;
      margin-right: auto;
      position: absolute;
      left: calc(100% - 55%);
      user-select: none;
      -moz-user-select: none;
      -ms-user-select: none;
      -webkit-user-drag: none;
      -webkit-user-select: none;
  }
  .hidden-pokemon {
      filter: brightness(0);
  }
</style>