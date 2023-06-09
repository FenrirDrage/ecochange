<script>
    import { createEventDispatcher } from 'svelte';
    // Define your menu items here
    let menuItems = [
      { icon: 'icon/rlocalon.svg', page: 'Home' },
      { icon: 'icon/reciclagem.svg', page: 'About' },
      { icon: 'icon/cardon.svg', page: 'Contact' },
      { icon: 'icon/rankingon.svg', page: 'Contact' },
      { icon: 'icon/accon.svg', page: 'Contact' },
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
      display: flex;
      background-color: #f0f0f0;
      padding: 10px;
    }
  
    .menu-item {
      display: flex;
      align-items: center;
      margin-right: 8px;
    }
  
    .icon {
      margin-right: 4px;
    }
  </style>
  
  <div class="menu">
    {#each menuItems as item}
    <a class="menu-item" href="" on:click={handleClick} data-page={item.page}>
        <img src={item.icon} alt={item.link} />
    </a>
    {/each}
  </div>
  