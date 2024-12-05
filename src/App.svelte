<script>
  import { Router, Route } from 'svelte-routing';
  import LibroIntercambio from "./routes/LibroIntercambio/LibroIntercambio.svelte";
  import Catalogo from "./routes/Catalogo/Catalogo.svelte";

 
</script>

<Router>
  <Route path="/" component={LibroIntercambio} />
  <Route path="/Catalogo" component={Catalogo} />
</Router>

