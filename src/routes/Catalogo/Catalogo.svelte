<script>
    import { onMount } from 'svelte';
    import Header from '../../components/Header/Header.svelte';
    import Footer from '../../components/Footer/Footer.svelte';
    import './Catalogo.css';
    
    let images = [];
    let isLoading = true;
    let cartBooks = [];
    let rows = [];
  
    // Cargar los libros del archivo JSON
    onMount(async () => {
      try {
        const response = await fetch('/assets/LibrosJson.json');
        
        // Comprobar si la respuesta es correcta
        if (!response.ok) {
          throw new Error(`Error al cargar el JSON: ${response.statusText}`);
        }
  
        // Convertir la respuesta a JSON
        images = await response.json();
        
        // Dividir las imágenes en filas de 8
        rows = [];
        if (images.length) {
          for (let i = 0; i < images.length; i += 8) {
            rows.push(images.slice(i, i + 8));
          }
        }
  
      } catch (error) {
        console.error('Error al cargar el JSON:', error);
      } finally {
        // Cambiar el estado de carga
        isLoading = false;
      }
  
      // Recuperar los libros almacenados en el carrito desde localStorage
      const storedCart = JSON.parse(localStorage.getItem('cart')) || [];
      cartBooks = storedCart;
    });
  

  </script>
  <Header/>
  <div class="Catalogo-father">
    <div class="Catalogo-body">
      {#if isLoading}
        <div class="loading">Cargando libros...</div>
      {:else}
        <div class="image-grid">
            <h1>CATALOGO</h1>
          {#each rows as row}
            <div class="row">
              {#each row as book}
                <div class="image-item">
                  <img src={book.imagen} alt={book.nombre} />
                  <div>
                  </div>
                </div>
              {/each}
            </div>
          {/each}
        </div>
      {/if}
    </div>
  </div>
  <Footer/>