<script>
  import PokedexCard from "../components/PokedexCard.svelte";
  import { onMount } from "svelte";
  //   import { pokeDetails } from "./+page";

  const kantoDex = "https://pokeapi.co/api/v2/pokedex/kanto/";

  const kantoAdditional = "https://pokeapi.co/api/v2/pokemon/";

  let pokemon = [];

  onMount(() => {
    async function fetchAPI() {
      const req = await fetch(kantoDex);

      const result = await req.json();
      console.log("list", result);

      pokemon = result.pokemon_entries;
      console.log("list", pokemon);

      const imgRequest = await fetchImage(pokemon);

      //   const imgResult = imgRequest;

      //   [0].pokemon_species.url

      console.log("iiiimmmmaaage", imgRequest);
    }

    fetchAPI();
  });

  async function fetchImage(arr) {
    const imageRequests = arr.map(async (poke) => {
      const imageReq = await fetch(poke.pokemon_species.url);
      const imageRes = await imageReq.json();
      return imageRes;
    });

    return Promise.all(imageRequests);
  }
</script>

<svelte:head>
  <title>Sveltemon</title>
</svelte:head>

{#each pokemon as poke}
  <PokedexCard name={poke.pokemon_species.name} />
{/each}
<section></section>

<style>
</style>
