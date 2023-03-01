<script>
  import { getContext } from "svelte";
  import { onMount } from "svelte";

  import Videojuego from "./Videojuego.svelte";
  import Boton from "./Boton.svelte";
  import Buscar from "./Buscar.svelte";

  import { data } from "./store.js";

  let videojuegoInsertar = {};

  let datosFiltrados = [];
  let patron = "";
  const URL = getContext("URL");

  let getVideojuegos = async () => {
    const response = await fetch(URL.videojuegos);
    $data = await response.json();
  };

  onMount(getVideojuegos);

  $: datosFiltrados = $data.filter((videojuego) =>
    RegExp(patron, "i").test(videojuego.titulo)
  );
</script>

<h1 class="titulo">Videojuegos <img src="/img/videojuego2.png" alt="videojuego" class="icons"></h1>
<div class="busqueda">
  Buscar:
  <Buscar bind:busqueda={patron} />
</div>

<hr />

<div class="container">
  <Videojuego bind:videojuego={videojuegoInsertar}>
    <div style="text-align: right">
      <Boton documento={videojuegoInsertar} />
    </div>
  </Videojuego>
</div>

<div class="container">
  {#each datosFiltrados as videojuego}
    <Videojuego bind:videojuego>
      <div style="text-align: right">
        <Boton tipo="modificar" documento={videojuego} />
        <Boton tipo="eliminar" documento={videojuego} />
      </div>
    </Videojuego>
  {/each}
</div>

<style>
  .container {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: left;
    flex-wrap: wrap;
  }
</style>
