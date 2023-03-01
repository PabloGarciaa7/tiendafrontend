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