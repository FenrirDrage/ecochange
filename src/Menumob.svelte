<script>
    import { createEventDispatcher } from 'svelte';
    // Define your menu items here
    let menuItems = [
      { text: 'Home', icon: 'home', page: 'Home' },
      { text: 'About', icon: 'info', page: 'About' },
      { text: 'Contact', icon: 'mail', page: 'Contact' },
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
    <a
      class="menu-item"
      href=""
      on:click={handleClick}
      data-page={item.page}
    >
    <span class="icon">{item.icon}</span>
    <span>{item.text}</span>
    </a>
    {/each}
  </div>
  