<script>
    import { onMount } from 'svelte';
    import { navigate } from 'svelte-routing';
    
    let isLoggedIn = false;
  
    // Verificar si el usuario está logueado al cargar el componente
    onMount(() => {
      const user = sessionStorage.getItem('idUsuario');
      isLoggedIn = !!user;
    });
  
    const handleLogout = () => {
      sessionStorage.removeItem('idUsuario');
      isLoggedIn = false;
      navigate('/login');
    };
  
    const handleLoginClick = () => {
      navigate('/login'); // Ir a la vista de login
    };
  
    const handleSignUpClick = () => {
      navigate('/registro'); // Ir a la vista de registro
    };
  
    const handleLogoClick = () => {
      navigate('/catalogo'); // Ir a la vista de catálogo
    };
  </script>
  
  <style>
    @import './Header.css';
  </style>
  
  <div class="header-container">
    <button on:click={handleLogoClick} class="header-icon_button">
      <img src="/LogoClaro.png" alt="logo" class="header-icon_container" />
    </button>
    <div class="botonesDer">
      <button class="header-button" on:click={() => navigate('/Catalogo')}>Tienda</button>
      <button class="header-button" on:click={() => navigate('/')}>Usuario</button>
    </div>
      

  </div>