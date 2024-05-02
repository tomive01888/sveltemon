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

<div class="container">
  {#await getPokemon()}
    <div class="loader"></div>
  {:then data}
    {#each data.results as pokemon, index}
      {#await getInfo(pokemon.url)}
        <p>..getting image</p>
      {:then details}
        <PokedexCard types={details.types} {index} name={pokemon.name} src={details.sprites.front_default} />
      {:catch error}
        <p>...error getting details {error.message}</p>
      {/await}
    {/each}
  {:catch error}
    <p>Error, something went wrong!</p>
  {/await}
</div>

<style>
  .container {
    display: grid;
    grid-template-columns: repeat(8, 1fr);
    gap: 10px;
    column-gap: 30px;
  }

  /* HTML: <div class="loader"></div> */
  .loader {
    height: 60px;
    aspect-ratio: 1;
    position: relative;
  }
  .loader::before,
  .loader::after {
    content: "";
    position: absolute;
    inset: 0;
    border-radius: 50%;
    transform-origin: bottom;
  }
  .loader::after {
    background:
      radial-gradient(at 75% 15%, #fffb, #0000 35%),
      radial-gradient(at 80% 40%, #0000, #0008),
      radial-gradient(circle 5px, #fff 94%, #0000),
      radial-gradient(circle 10px, #000 94%, #0000),
      linear-gradient(#f93318 0 0) top / 100% calc(50% - 5px),
      linear-gradient(#fff 0 0) bottom/100% calc(50% - 5px) #000;
    background-repeat: no-repeat;
    animation: l20 1s infinite cubic-bezier(0.5, 120, 0.5, -120);
  }
  .loader::before {
    background: #ddd;
    filter: blur(8px);
    transform: scaleY(0.4) translate(-13px, 0px);
  }
  @keyframes l20 {
    30%,
    70% {
      transform: rotate(0deg);
    }
    49.99% {
      transform: rotate(0.2deg);
    }
    50% {
      transform: rotate(-0.2deg);
    }
  }
</style>
