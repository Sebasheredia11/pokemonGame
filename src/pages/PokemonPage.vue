<template>
    <div>
        <h1>¿Quiene es este Pokemon?</h1>
        
        <pokemon-picture :pokemonId="6" :showPokemon="true" />
        <pokemon-options :pokemons="pokemonArr" />
    </div>
</template>

<script>
import PokemonOptions from '@/components/PokemonOptions.vue'
import PokemonPicture from '@/components/PokemonPicture.vue'

import getPokemonOptions from '@/helpers/getPokemonOptions'

// console.log(getPokemonOptions());


export default {
    name: 'PokemonPage',
    components: {
        PokemonOptions,
        PokemonPicture
    },
    data(){
        return{
            pokemonArr: []
        }
    },
    methods: {
        async mixPokemonArray(){
            this.pokemonArr = await getPokemonOptions();
        }
    },

    mounted(){
        this.mixPokemonArray()
    }
}
</script>
