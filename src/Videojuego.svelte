<script>
    export let videojuego = { titulo: "", genero: "" };
  </script>
  
  <div class="card">
    <input
      type="text"
      placeholder="Titulo"
      bind:value={videojuego.titulo}
      class="title" />
    <input type="text" placeholder="Genero" bind:value={videojuego.genero} class="title"/> 
    <span class="title">€</span>
    <slot />
  </div>
  
  <style>
    .title {
      color: white;
    }
    .card {
      background-color: #4e7dfc;
      box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.384);
      border-radius: 5px;
      transition: 0.3s;
      padding: 10px;
      margin: 10px;
    }
    .card:hover {
      box-shadow: 0 8px 16px 0 rgba(27, 236, 236, 0.733);
    }
    input {
      background-color: inherit;
      padding: 10px;
      font-size: 14px;
      color: black;
      border: 0;
      outline: none;
      margin-left: 5px;
      margin-bottom: 4px;
      max-width: 140px;
    }
    input:focus {
      color: black;
      background-color: rgb(255, 255, 255);
    }
    input:required:invalid,
    input:focus:invalid {
      background-color: lightpink;
    }
  </style>
  