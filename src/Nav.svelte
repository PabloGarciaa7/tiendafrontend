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
    nav{
        background-color: rgb(159, 176, 255);
        padding: 15px;
    }

    ul{
        display: flex;
        justify-content: space-around;
        list-style-type: none;
    }
    
</style>