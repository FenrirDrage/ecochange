<script>
  import {
    Collapse,
    Navbar,
    NavbarToggler,
    NavbarBrand,
    Nav,
    NavItem,
    NavLink,
    Dropdown,
    DropdownToggle,
    DropdownMenu,
    DropdownItem
  } from 'sveltestrap';
  import Menupc from './Menupc.svelte';
  import Menumob from './Menumob.svelte';
  import Login from './checklog.svelte';
  import { onMount } from 'svelte';
  import { initializeApp } from 'firebase/app';
  import { getAuth } from 'firebase/auth';
  import { firebaseConfig } from './firebaseConfig.js';
  
  let isMobile = false;
  let isLoggedIn = false;

  // Initialize Firebase app
  const app = initializeApp(firebaseConfig);

  // Get the Firebase auth instance
  const auth = getAuth(app);

  onMount(() => {
    const mediaQuery = window.matchMedia('(max-width: 768px)');
    isMobile = mediaQuery.matches;

    const handleResize = (event) => {
      isMobile = event.matches;
    };

    mediaQuery.addEventListener('change', handleResize);

    return () => {
      mediaQuery.removeEventListener('change', handleResize);
    };
  });

  let currentPage = '';
  
  onMount(() => {
    currentPage = 'Cards';
  });

  onMount(() => {
  // Check if the user is already logged in
  const unsubscribe = auth.onAuthStateChanged((user) => {
    isLoggedIn = user ? true : false;
  });
    return () => {
      unsubscribe();
    };
  });

  function updatePage(event) {
    currentPage = event.detail.page;
  }

  function logIn() {
  const email = document.getElementById("email").value;
  const password = document.getElementById("password").value;

  signInWithEmailAndPassword(auth, email, password)
    .then((result) => {
      isLoggedIn = true;
      const user = result.user;
      // Additional logic after successful login
    })
    .catch((error) => {
      const errorCode = error.code;
      const errorMessage = error.message;
      // Handle login error
    });
  }

  function logOut() {
    signOut(auth)
      .then(() => {
      isLoggedIn = false;
      // Additional logic after successful logout
    })
    .catch((error) => {
      // Handle logout error
    });
  }
</script>

<style>
  .container {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-color: #6acc6a;
  }

  .menu {
    background-color: #1f6807;
    padding: 16px;
    border-radius: 8px;
    margin-right: 16px;
  }

  .bar {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    background-color: #1f6807;
    color: #fff;
    padding: 8px;
    text-align: center;
    z-index: 9999;
    font-family: Montserrat;
  }

  .card-container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: calc(100vh - 40px); /* Subtract the height of the bar */
    margin-top: 40px; /* Adjust the margin to account for the height of the bar */
  }

  .card {
    background-color: #f1f1f1;
    padding: 16px;
    border-radius: 8px;
  }

  @media (min-width: 769px) {
    /* Desktop styles */
    .menu {
      position: fixed;
      left: 0;
      margin-right: 0;
      margin-bottom: 16px;
    }
  }

  @media (max-width: 768px) {
    /* Mobile styles */
    .menu {
      position: fixed;
      bottom: 0;
      margin-right: 16px;
    }
  }
</style>

<div class="container">
  
  {#if isMobile}
    <div class="menu"><Menumob on:itemSelected={updatePage} /></div>
  {:else}
    <div class="menu"><Menupc on:itemSelected={updatePage} /></div>
  {/if}

  <div class="bar">{currentPage}</div>

  <main>
    
    {#if currentPage === 'Local'}
      
      <p>WIP locais a recliclar</p>
    {/if}
    {#if currentPage === 'Recicle'}
      
      <p>WIP a reciclar</p>
    {/if}
    {#if currentPage === 'Cards'}
      {#if isLoggedIn}
        <div class="card-container">
          <a href="" class="menu-link">
            <div class="card">
              <h1>+</h1>
              <h2>Adicionar Cartão</h2>
            </div>
          </a>
        </div>
      {:else}
        <div class="card-container">
          <a href="" class="menu-link" on:click={() => currentPage = 'Login'}>
            <div class="card">
              <h1>+</h1>
              <h2>Adicionar Cartão</h2>
            </div>
          </a>
        </div>
      {#if currentPage === 'Login'}
      <Login />
      {/if}
      {/if}
    {/if}
    {#if currentPage === 'Ranking'}
      
      <p>WIP Ranks</p>
    {/if}
    {#if currentPage === 'User'}
      
      <p>WIP a tua conta</p>
    {/if}
  </main>
</div>