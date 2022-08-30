<template>
  <div class="options-container">
    <ul>
      <li v-for="pokemon in pokemons" :key="pokemon.id" @click="$emit('selectionPokemon', pokemon.id)">{{
          pokemon.name
        }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "PokemonOptions",
  props: {
    pokemons: {
      type: Array,
      required: true,
    }
  }

}
</script>

<style scoped>

ul {
  padding: 0;
  list-style-type: none;
}

li {
  background-color: white;
  border-radius: 8px;
  border: 1px dashed rgba(0, 0, 0, 0.2);
  cursor: pointer;
  margin-bottom: 10px;
  padding: 5px;
  width: 250px;
  text-transform: capitalize;
  font-size: 1em;
  font-weight: bold;
}

li:hover {
  background-color: #FFFFCC;
}

.options-container {
  display: flex;
  justify-content: center;
}
</style>
