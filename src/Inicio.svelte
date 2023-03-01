<script>
    import { Link } from "svelte-routing";
</script>
<h1 class="titulo">Tienda Gamer <img src="/img/videojuego.png" alt="consola" class="icons"></h1>

<hr>

<Link to="/videoconsolas">
    <div class="opcion">Operaciones CRUD con Videoconsolas <img src="/img/videoconsola.png" alt="consola" class="icons"></div>
</Link>

<Link to="/videojuegos">
    <div class="opcion">Operaciones CRUD con Videojuegos <img src="/img/videojuego2.png" alt="videojuego" class="icons"></div>
</Link>


