<template>
  <h1 v-if="!pokemon">Loading ...</h1>
  <div v-else>
    <h1>What Pokemon is this?</h1>

    <PokemonPicture :pokemonId="pokemon.id" :showPokemon="showPokemon"/>
    <div v-if="showOptions">
      <PokemonOptions :pokemons="pokemonArr" @selectionPokemon="checkAnswer($event)"/>
    </div>
  </div>

  <template v-if="showAnswer">
    <h2 :style="{color: colorResult}">{{ message }}</h2>
    <button @click="newGame">Next</button>
  </template>

  <footer>
    <div>Eric Weber: <a href="https://ewvl.net" target="_blank">https://ewvl.net</a> | <a
        href="https://www.linkedin.com/in/eric-weber"
        target="_blank">https://www.linkedin.com/in/eric-weber</a>
    </div>
    <div>Source: Fernando Herrera | <a href="https://fernando-herrera.com/#/courses/Frontend"
                                       target="_blank">https://fernando-herrera.com</a>
    </div>
  </footer>
</template>

<script>
import PokemonPicture from "@/components/PokemonPicture";
import PokemonOptions from "@/components/PokemonOptions";

import getPokemonOptions from '@/helpers/getPokemonOptions'

export default {
  name: "PokemonPage",
  components: {PokemonPicture, PokemonOptions},
  data() {
    return {
      pokemonArr: [],
      pokemon: null,
      showPokemon: false,
      showAnswer: false,
      showOptions: true,
      title: '',
      message: '',
      colorResult: 'red',
    }
  },
  methods: {
    async mixPokemonArray() {
      this.pokemonArr = await getPokemonOptions()
      const rndInt = Math.floor(Math.random() * 4)
      this.pokemon = this.pokemonArr[rndInt]
    },

    checkAnswer(selectedId) {
      this.showPokemon = true
      this.showAnswer = true
      this.showOptions = false

      if (selectedId === this.pokemon.id) {
        this.colorResult = 'green'
        this.message = `Congratulations!! ${this.pokemon.name}`
      } else {
        this.colorResult = 'red'
        this.message = `Wrong!! ${this.pokemon.name}`
      }
    },

    newGame() {
      this.showPokemon = false
      this.showAnswer = false
      this.showOptions = true
      this.message = ''
      this.pokemonArr = []
      this.pokemon = null
      this.mixPokemonArray()
    }
  },
  mounted() {
    this.mixPokemonArray()
  }
}
</script>

<style scoped>
h2 {
  font-size: 2em;
  color: red;
  text-transform: capitalize;
}

button {
  background-color: #2279FF;
  border-radius: 5px;
  border: none;
  border-right: 2px solid #FFFF00;
  border-bottom: 2px solid #FFFF00;
  padding: 5px 16px;
  color: white;
  font-size: 1.5em;
  font-weight: bold;
  margin-bottom: 20px;
  cursor: pointer;
}

.score {
  width: 30%;
  margin: 10px auto;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.score > * {
  font-size: 3em;
  font-weight: bold;
}

.greens {
  color: green;
}

.reds {
  color: red;
}

footer {
  position: fixed;
  border-top: 3px solid #999;
  padding: 10px 0;
  left: 0;
  bottom: 0;
  width: 100%;
  background-color: #CCC;
  color: #333;
  text-align: center;
  font-size: 0.75em;
}
</style>
