<script>
    import { createEventDispatcher } from 'svelte';
    // Define your menu items here
    let menuItems = [
      { text: 'Local', icon: 'icon/rlocalon.svg', page: 'Local' },
      { text: 'Reciclagem', icon: 'icon/reciclagem.svg', page: 'Recicle' },
      { text: 'Cartoes', icon: 'icon/cardon.svg', page: 'Cards' },
      { text: 'Ranking', icon: 'icon/rankingon.svg', page: 'Ranking' },
      { text: 'Utilizador', icon: 'icon/accon.svg', page: 'User' },
    ];

    let selectedItem = null;
    const dispatch = createEventDispatcher();

    function selectItem(page, event) {
    selectedItem = page;
    dispatch('itemSelected', { page });
    event.stopPropagation();
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
      padding: 10px;
      background-color: #1f6807;
    }
  
    .menu-item {
      display: flex;
      align-items: center;
      margin-right: 8px;
      background-color: #1f6807; /* Set the background color to green */
      padding: 8px; /* Optional: Adjust the padding as needed */
      border-radius: 4px; /* Optional: Add border radius for a rounded look */
      transition: transform 0.3s ease; /* Add transition for smooth animation */
    }

    .menu-item.selected {
    transform: translateY(-15px); /* Slide up the image by 8px when selected */
    }
  
    .icon {
      margin-right: 4px;
    }
  </style>
  
  <div class="menu">
    {#each menuItems as item}
    <a class="menu-item {selectedItem === item.page ? 'selected' : ''}" href="" on:click|preventDefault|stopPropagation={selectItem.bind(null, item.page)}>
        <img src={item.icon} alt={item.link} />
      </a>
    {/each}
  </div>