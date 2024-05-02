<script>
  let name = "lols";
  const KANTO_REGION = "kanto";

  async function getDex() {
    const request = await fetch(`https://pokeapi.co/api/v2/pokedex/${KANTO_REGION}`);
    const data = await request.json();
    console.log("asdasdasd",data);
  }

  const wut = getDex();
</script>

<h1>Hello from {name}</h1>
