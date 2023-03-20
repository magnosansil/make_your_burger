<template>
  <div class="home">
    <nav class="navbar navbar-expand-lg">
      <div class="container-fluid">        
        <img :src="logo" :alt="alt" id="logo" title="Make Your Burger">
        <a href="/">
          <h1 id="main_title">Make Your Burger</h1>
        </a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
          <div class="navbar-nav">            
            <router-link to="/" id="logo_url" class="nav-link"></router-link>         
            <router-link to="/" class="nav-link">Home</router-link>
            <router-link to="/pedidos" id="link_pedidos" class="nav-link">Pedidos</router-link>            
          </div>
        </div>        
      </div>
    </nav>
  </div> 
</template>

<script>
  export default {
    name: 'Navbar',
    props: ['logo', 'alt']
  }
</script>

<style scoped>
  nav {
    background-color: #222;
    border-bottom: 4px solid;
    border-image: linear-gradient(to right, #f82410, #4d0000);
    border-image-slice: 1;
    padding: 0 50px;
    display: flex;
    align-items: center;
  }

  #logo_url {
    margin: auto;
  }

  #logo {
    width: 40px;
    height: 40px;
  }

  #main_title {
    color: #fcba03;
    font-size: 30px;
    margin-top: auto; 
    margin-bottom: auto;
  }

  /* #link_pedidos {
    pointer-events: none;
    cursor: default;
  } */

  nav a {
    color: #fcba03;
    text-decoration: none;
    margin: 12px;
    transition: 0.5s;
  }

  nav a:hover {
    color: #f5f5fa;
  }

  .navbar-toggler {
    border-color: transparent;
  }
  .navbar-toggler-icon {
    background-image: url("data:image/svg+xml;charset=utf8,%3Csvg viewBox='0 0 32 32' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath stroke='rgba(252, 186, 3)' stroke-width='2' stroke-linecap='round' stroke-miterlimit='10' d='M4 8h24M4 16h24M4 24h24'/%3E%3C/svg%3E");
  }

  .navbar-toggler:hover {
    border-color: #f5f5fa;
  }
  .navbar-toggler-icon:hover {
    background-image: url("data:image/svg+xml;charset=utf8,%3Csvg viewBox='0 0 32 32' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath stroke='rgba(245, 245, 250)' stroke-width='2' stroke-linecap='round' stroke-miterlimit='10' d='M4 8h24M4 16h24M4 24h24'/%3E%3C/svg%3E");
  }

  @media (max-width: 510px) {
    nav {
      padding: 0;
    }

    #main_title {
      font-size: 20px;
    }

    #logo {
      display: none
    }
  }
</style> 
