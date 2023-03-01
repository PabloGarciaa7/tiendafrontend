<script>
  import { getContext } from "svelte";
  import { onMount } from "svelte";

  import Videoconsola from "./Videoconsola.svelte";
  import Boton from "./Boton.svelte";
  import Buscar from "./Buscar.svelte";
  import { data } from "./store.js";
  let videoconsolaInsertar = {};

  let datosFiltrados = [];
  let patron = "";
  const URL = getContext("URL");

  let getVideoconsolas = async () => {
    const response = await fetch(URL.videoconsolas);
    $data = await response.json();
  };

  onMount(getVideoconsolas);

  $: datosFiltrados = $data.filter((videoconsola) =>
    RegExp(patron, "i").test(videoconsola.nombre)
  );
</script>

<h1 class="titulo">Videoconsolas <img src="/img/videoconsola.png" alt="consola" class="icons"></h1>
<div class="busqueda">
  Buscar:
  <Buscar bind:busqueda={patron} />
</div>

<hr />

<div class="container">
  <Videoconsola bind:videoconsola={videoconsolaInsertar}>
    <div style="text-align: right">
      <Boton coleccion="videoconsolas" documento={videoconsolaInsertar} />
    </div>
  </Videoconsola>
</div>

<div class="container">
  {#each datosFiltrados as videoconsola}
    <Videoconsola bind:videoconsola>
      <div style="text-align: right">
        <Boton
          coleccion="videoconsolas"
          tipo="modificar"
          documento={videoconsola}
        />
        <Boton
          coleccion="videoconsolas"
          tipo="eliminar"
          documento={videoconsola}
        />
      </div>
    </Videoconsola>
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
