<template>
    <h1 v-if="!pokemon">Espere por favor...</h1>

    <div v-else>
        <h1>¿Quien es este Pokemon?</h1>
        
        <pokemon-picture :pokemonId="pokemon.id" :showPokemon="showPokemon" />
        <pokemon-options 
            :pokemons="pokemonArr" 
            @click="checkAnswer(1,$event)"    
        />

        <div v-if="showAnswer">
            <h2 class="fade-in"> {{message}} </h2>
            <button @click="newGame">
                Nuevo Juego
            </button>
        </div>
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
            pokemonArr: [],
            pokemon: null,
            showPokemon: false,
            showAnswer: false,
            message: ''
        }
    },
    methods: {
        async mixPokemonArray(){
            this.pokemonArr = await getPokemonOptions()
            const rndInt = Math.floor(Math.random() * 4)
            console.log(rndInt);
            this.pokemon = this.pokemonArr[rndInt]
        },
        checkAnswer(selectedId){
            this.showPokemon = true
            this.showAnswer = true

            if(selectedId === this.pokemon.id){
                this.message = `Correcto, ${this.pokemon.name}`
            }else{
                this.message = `Incorrecto, ${this.pokemon.name}`
            }
        },

        newGame(){
            this.showPokemon = false
            this.showAnswer = false
            this.message = ''
            this.mixPokemonArray()
        }
    },

    mounted(){
        this.mixPokemonArray()
    }
}
</script>
