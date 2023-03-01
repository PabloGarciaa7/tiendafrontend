<script>
    import Nav from "./Nav.svelte";
	import { Router } from "svelte-routing";
    import Contenido from "./Contenido.svelte";
    import { setContext } from "svelte";
  import Footer from "./Footer.svelte";

	const URL = {
		videoconsolas:"https://tiendabackend-txsi.onrender.com/api/videoconsolas",
		videojuegos:"https://tiendabackend-txsi.onrender.com/api/videojuegos"
	}

	setContext("URL",URL)
</script>


<Router>
	<Nav />
	<Contenido />
  <Footer/>
</Router>


<style>
  :global(*) {
    margin: 0;
    padding: 0;
  }

  :global(body) {
    margin: 0;
    padding: 0;
    display: flex;
    flex-direction: column;
    font-display: swap;  
	background-color: rgba(41, 41, 136, 0.644);   
  }
 
  :global(a:hover) {
    text-decoration: none;
    cursor: pointer;
  }

</style>