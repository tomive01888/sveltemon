<script>
  export let name = "";
  export let src = "";
</script>

<div class="pokecard">
  <img {src} alt={name} />
  <p>{name}</p>
</div>

<style>
  p {
    color: red;
  }
</style>
