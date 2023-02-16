<script setup>
import { reactive, ref, computed, onMounted } from 'vue'

const pokemonStore = reactive({
  list: [],
  filteredList: computed(() => 
    pokemonStore.list.filter(pokemon => 
      pokemon.pokemon_species.name.includes(filterText.value)
    )
  )
})

const filterText = ref('')

onMounted( async () => {
  const pokeData = await fetch('https://pokeapi.co/api/v2/pokedex/2/').then(
      response => response.json()
  )
  pokemonStore.list = pokeData.pokemon_entries
})

// export default {
//   data: () => ({
//     pokemonList: []
//   }),
//   async mounted() {
//     const pokeData = await fetch('https://pokeapi.co/api/v2/pokedex/2/').then(
//       response => response.json()
//     )
//     this.pokemonList = pokeData.pokemon_entries
//     console.log({ pokeData })
//   }
// }
</script>

<template>
  <main>
    <h1 class="text-3xl font-bold mb-4">Gabe's Pokedex</h1>
    <div class="flex flex-col">
      <label for="search-pokemon" class="block mb-2 text-sm">Search Pokemon</label>
      <input type="text" v-model="filterText" class="block w-full text-gray-600 rounded-sm p-2 focus:ring-emerald-600 focus:border-emerald-600 mb-8">
      <!-- <button class="block text-white py-2 px-4 rounded-sm bg-violet-600 mt-4 font-bold">Search Pokemon</button> -->
    </div>
    <article v-for="(pokemon, index) in pokemonStore.filteredList" :key="`poke-${index}`" class="flex flex-col mt-4 justify-center p-6 bg-zinc-300 rounded-sm shadow-sm">
      <p>{{ pokemon.type.name }}</p>
      <p class="text-lg text-stone-700">#{{ pokemon.entry_number }} - {{ pokemon.pokemon_species.name }}</p>
    </article>

    <!-- <ul>
      <li v-for="(pokemon, index) in pokemonStore.filteredList" :key="`poke-${index}`">#{{ pokemon.entry_number }} - {{ pokemon.pokemon_species.name }}</li>
      <PokeCard v-for="(pokemon, index) in pokemonStore.filteredList" :key="`poke-${index}`" :number="pokemon.entry_number" :name="pokemon.pokemon_species.name"/>
    </ul> -->

  </main>
</template>
