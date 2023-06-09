<script>
  import { createEventDispatcher } from 'svelte';
    // Define your menu items here
    let menuItems = [
      { text: 'Local',icon: 'icon/rlocalon.svg', page: 'Home' },
      { text: 'Reciclagem',icon: 'icon/reciclagem.svg', page: 'About' },
      { text: 'Cartoes',icon: 'icon/cardon.svg', page: 'Contact' },
      { text: 'Ranking',icon: 'icon/rankingon.svg', page: 'Contact' },
      { text: 'Utilizador',icon: 'icon/accon.svg', page: 'Contact' },
    ];
    const dispatch = createEventDispatcher();

    function selectItem(page) {
    dispatch('itemSelected', { page });
    }
    
    function handleClick(event) {
    event.preventDefault();
    event.stopPropagation();
    const page = event.currentTarget.getAttribute('data-page');
    selectItem(page);
    }
  </script>
  
  <style>
    .menu {
      background-color: #f0f0f0;
      padding: 10px;
    }
  
    .menu-item {
      display: flex;
      align-items: center;
      margin-bottom: 8px;
    }
  
    .icon {
      margin-right: 8px;
    }
  </style>
  
  <div class="menu">
    {#each menuItems as item}
    <a
      class="menu-item"
      href=""
      on:click={handleClick}
      data-page={item.page}
    >
    <img src={item.icon} alt={item.link} />
    <span>{item.text}</span>
    </a>
    {/each}
  </div>
  