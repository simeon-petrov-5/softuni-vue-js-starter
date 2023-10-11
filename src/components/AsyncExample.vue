<script>
import { useAsyncState } from '@vueuse/core'

const apiUrl = 'https://pokeapi.co/api/v2/pokemon/'
async function fetchPokemonData() {
  try {
    // Use the Fetch API with async/await
    const response = await fetch(apiUrl)

    // Check if the response status is OK (status code 200)
    if (!response.ok)
      throw new Error('Network response was not ok')

    // Parse the JSON response
    const data = await response.json()

    // Handle the data from the API
    console.log('Pokemon Data:', data)
    return data.results
  }
  catch (error) {
    // Handle any errors that occurred during the fetch
    console.error('Error:', error)
  }
}
export default {
  setup() {
    const {
      state: pokemons,
      isReady,
      isLoading,
    } = useAsyncState(fetchPokemonData(), [])
    return { pokemons, isReady, isLoading }
  },
  //   data() {
  //     return {
  //       pokemons: [],
  //     };
  //   },
  //   created() {
  //     fetchPokemonData().then((data) => (this.pokemons = data));
  //   },
}
</script>

<template>
  <div>HERE I AM</div>
  <span>{{ isReady }}</span>
  <ul>
    <li v-for="pokemon in pokemons" :key="pokemon.name">
      {{ pokemon.name }}
    </li>
  </ul>
</template>

<style lang="scss" scoped></style>
