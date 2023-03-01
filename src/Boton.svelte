<script>
  import { getContext } from "svelte";
  import { onMount } from "svelte";
  import { data } from "./store";

  export let tipo = "insertar";
  export let documento = {};
  export let coleccion = "";
  let clases = "";

  let handler = () => {};
  let URL = getContext("URL");

  let direccion = "";
  

  if (coleccion == "videoconsolas") {
    direccion = URL.videoconsolas;
  }else {
    direccion = URL.videojuegos;
  }

  function insertar() {
    let opciones = {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(documento)
    };

    fetch(direccion, opciones)
      .then((res) => res.json())
      .then( doc => $data = [...$data,doc])
      .catch((err) => {
        console.log(err);
      });
  }

  function modificar() {
    let opciones = {
    method: "PUT",
      headers: { "Content-Type": "application/json" },
        body: JSON.stringify(documento )
    };

    fetch(direccion + "/" + documento._id, opciones)
      .then(res => res.json())
      .catch((err) => {
        console.log(err);
      });
  }

  function eliminar() {
    let opciones = {
      method: "DELETE",
    };

    fetch(direccion + "/" + documento._id, opciones)
      .then((res) => res.json())
      .then($data = $data.filter(doc => doc._id != documento._id))
      .catch((err) => {
        console.log(err);
      });
  }

  function setup() {
    switch (tipo) {
      case "insertar":
        handler = insertar;
        clases = "insertar";
        break;
      case "modificar":
        handler = modificar;
        clases = "modificar";
        break;
      case "eliminar":
        handler = eliminar;
        clases = "eliminar";
        break;
      default:
        break;
    }
  }

  onMount(setup);

</script>

<input type="button" class={clases} value={tipo.toLocaleUpperCase()} on:click={handler} />
