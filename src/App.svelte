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
  import { onMount } from 'svelte';
  

  let isMobile = false;

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
    currentPage = 'Home';
  });

  function updatePage(event) {
    currentPage = event.detail.page;
  }

</script>

<style>
  .container {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }

  .menu {
    background-color: #ccc;
    padding: 16px;
    border-radius: 8px;
    margin-right: 16px;
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

  <main>
    {#if currentPage === 'Home'}
      <h1>Welcome to the Home Page</h1>
    {/if}
    {#if currentPage === 'About'}
      <h1>About Us</h1>
      <p>This is the about page content.</p>
    {/if}
    {#if currentPage === 'Contact'}
      <h1>Contact Us</h1>
      <p>Feel free to get in touch with us.</p>
    {/if}
  </main>
</div>
