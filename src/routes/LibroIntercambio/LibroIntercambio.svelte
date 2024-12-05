<script>
// @ts-nocheck

    import { onMount } from 'svelte';
    import Header from '../../components/Header/Header.svelte';
    import Footer from '../../components/Footer/Footer.svelte';
    import './LibroIntercambio.css'
  
    let libreria = [];
    let pedidos = [];
    let isLoading = true;
    let error = null;
  
    const fetchLibros = async () => {
      try {
        const response1 = await fetch('/assets/usuario1.json');
        const response2 = await fetch('/assets/usuario2.json');
  
        if (!response1.ok || !response2.ok) {
          throw new Error('Error al cargar los archivos JSON');
        }
  
        const data1 = await response1.json();
        const data2 = await response2.json();
  
        libreria = data1.propios.map((libro) => ({
          ...libro,
          coincidencias: data2.querer.filter((l) => l.ISBN === libro.ISBN).length,
        }));
  
        pedidos = data1.querer.map((libro) => ({
          ...libro,
          coincidencias: data2.propios.filter((l) => l.ISBN === libro.ISBN).length,
        }));
      } catch (err) {
        error = err.message;
      } finally {
        isLoading = false;
      }
    };
  
    onMount(fetchLibros);
  </script>
  
  <div class="libros-intercambio">
    <Header />
  
    <main class="libros-contenedor">
        
        <!-- Sección Librería -->
        <div class="seccion">
          <h2>Librería</h2>
          <div class="grid">
            {#each libreria as libro, index}
              
            <div
            class="cuadro"
            tabindex="0"
            role="button"
            on:click={() => libro.coincidencias > 0 && navigate(`/intercambio/${libro.ISBN}/libreria`)}
            on:keydown={(e) => {
              if ((e.key === 'Enter' || e.key === ' ') && libro.coincidencias > 0) {
                navigate(`/intercambio/${libro.ISBN}/libreria`);
              }
            }}
            aria-label={`Abrir libro: ${libro.nombre}`}
          >
            <div class="imagen-contenedor">
              <img src={libro.imagen} alt={libro.nombre} />
              {#if libro.coincidencias > 0}
                <span class="coincidencia">{libro.coincidencias}</span>
              {/if}
            </div>
          </div>
            {/each}
          </div>
        </div>
    
        <!-- Sección Pedidos -->
        <div class="seccion">
            <h2>Pedidos</h2>
            <div class="grid">
              {#each pedidos as libro, index}
                <div
                  class="cuadro"
                  tabindex="0"
                  role="button"
                  aria-label={`Abrir libro pedido: ${libro.nombre}`}
                  on:click={() => libro.coincidencias > 0 && navigate(`/intercambio/${libro.ISBN}/pedido`)}
                  on:keydown={(e) => {
                    if ((e.key === 'Enter' || e.key === ' ') && libro.coincidencias > 0) {
                      navigate(`/intercambio/${libro.ISBN}/pedido`);
                    }
                  }}
                >
                  <div class="imagen-contenedor">
                    <img src={libro.imagen} alt={libro.nombre} />
                    {#if libro.coincidencias > 0}
                      <span class="coincidencia">{libro.coincidencias}</span>
                    {/if}
                  </div>
                </div>
              {/each}
            </div>
          </div>
      </main>
  
    <Footer />
  </div>
  