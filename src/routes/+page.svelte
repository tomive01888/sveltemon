<script>
  import PokedexCard from "../components/PokedexCard.svelte";

  const originalPokemon = "https://pokeapi.co/api/v2/pokemon?limit=151";

  const getPokemon = async () => {
    const request = await fetch(originalPokemon);
    const data = await request.json();
    return data;
  };

  const getInfo = async (urlToFetch) => {
    if (!urlToFetch) return;
    const req = await fetch(urlToFetch);
    const details = await req.json();
    return details;
  };
</script>

<svelte:head>
  <title>Sveltemon</title>
</svelte:head>

{#await getPokemon()}
  <p>...fetching</p>
{:then data}
  {#each data.results as pokemon}
    {#await getInfo(pokemon.url)}
      <p>..getting image</p>
    {:then details}
      <PokedexCard name={pokemon.name} src={details.sprites.front_default} />
    {:catch error}
      <p>...error getting details {error.message}</p>
    {/await}
  {/each}
{:catch error}
  <p>Error, something went wrong!</p>
{/await}

<style>
</style>
