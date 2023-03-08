# FRONTEND (con Svelte)

---

# Introducción

Este es el frontend de una aplicación, la cual consta de un repositorio donde se aloja el [backend](https://github.com/PabloGarciaa7/tiendabackend) y este repositorio el [frontend](https://github.com/PabloGarciaa7/tiendafrontend)

# Proyecto

El proyecto consiste en una tienda de videojuegos y videoconsolas. En el backend podemos ver la api y la documentación.

![GitHub Logo](/public/img/back.png)

La parte de frontend se ha creado con Svelte.

Si usamos el comando `tree`, esta es la estructura que tendria

```
├───public
│   └───img
├───scripts
└───src
```
En public se aloja todo lo relativo a la parte de estilos, y el propio html y en src, es donde se trabajará con Svelte. Svelte trabaja por componentes y en esta carpeta se crearán todos los componentes a utilizar, donde `App.svelte` será el componente principal de la aplicación.

Cada componente dispone de 3 secciones:

```html
<script>
  // Código javascript
</script>

<!-- Nuestros elementos HTML y componentes web -->

<style>
  /* Código CSS */
</style>
```

El orden es indiferente.

La estructura del componente `App` está formada por un `Router`, dentro del cual se definen dos componentes: `Nav`, que tendrá los enlaces (`Link`) necesarios para la navegación, y `Contenido`, que tendrá las rutas (`Routes`) a los componentes necesarios.

**`Nav.svelte`**

```html
<script>
    import { Link } from "svelte-routing";
</script>

<nav>
	<ul>
		<li><Link to="/">Inicio</Link></li>
		<li><Link to="/videoconsolas">Videoconsolas</Link></li>
		<li><Link to="/videojuegos" >Videojuegos</Link></li>
	</ul>
</nav>

<style>
    /* Aquí el código CSS para diseño responsive de la barra de navegación. */
    /* Consultar el código fuente */
</style>
```

El componente `Nav` será la barra de navegación (`nav`), con los enlaces a las rutas del lado cliente. Para los enlaces hacemos uso del componente `Link` del paquete `svelte-routing`.

**`Contenido.svelte`**

```html
<script>
    import { Route } from "svelte-routing";
    import Videoconsolas from "./Videoconsolas.svelte";
    import Videojuegos from "./Videojuegos.svelte";
    import Inicio from "./Inicio.svelte";
</script>
<main>
    <Route path="/" component="{Inicio}"></Route>
    <Route path="/videoconsolas" component="{Videoconsolas}"></Route>
    <Route path="/videojuegos" component="{Videojuegos}"></Route>
</main>
```

El componente `Contenido` será la sección principal (`main`), con las rutas y el componente asociado a cada una de ellas. Para las rutas hacemos uso del componente `Route` del paquete `svelte-routing`.

## Componentes para el contenido

Dentro del componente anterior `Contenido` podrán renderizarse distintos componentes, dependiendo del `Link` que pulsemos en la barra de navegación. Los componentes que podrán aparecer en `Contenido` son:

- **Inicio**
- **Videoconsolas**
- **Videojuegos**

**`Inicio.svelte`**

```html
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


```

**`Videoconsolas.svelte`**

 ```html
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

```



**`Videojuegos.svelte`**

```html
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

```
