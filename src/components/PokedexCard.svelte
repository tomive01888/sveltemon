<script>
  export let name = "";
  export let src = "";
  export let index = "";
  export let types = [];
</script>

<a href="/pokemon?index={index}" class="pokecard">
  <span class="idx">#{index + 1}</span>
  <img class="pokeImg" {src} alt={name} />
  <p>{name}</p>
  {#if types.length}
    <div class="type-box">
      {#each types as t}
        <img class="types" src={`types/${t.type.name}.ico`} alt={t.type.name} />
      {/each}
    </div>
  {/if}
</a>

<style>
  .type-box {
    display: flex;
    gap: 5px;
    position: absolute;
    top: 5px;
    right: 5px;
  }
  .types {
    width: 22px;
    height: auto;
    display: inline-block;
  }
  .idx {
    position: absolute;
    left: 5px;
    top: 5px;
    color: white;
  }

  .pokecard {
    position: relative;
    width: 100%;
    background-color: rgba(54, 54, 255, 0.841);
    border: 1px solid black;
    border-radius: 8px;
    display: grid;
    place-items: center;
    user-select: none;
    padding: 10px;
  }

  p {
    color: white;
    text-transform: capitalize;
  }

  .pokeImg {
    margin-top: 18px;
  }
</style>
