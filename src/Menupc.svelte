<script>
  import { createEventDispatcher } from 'svelte';

  let menuItems = [
    { text: 'Local', icon: 'icon/rlocalon.svg', page: 'Local' },
    { text: 'Reciclagem', icon: 'icon/reciclagem.svg', page: 'Recicle' },
    { text: 'Cartoes', icon: 'icon/cardon.svg', page: 'Cards' },
    { text: 'Ranking', icon: 'icon/rankingon.svg', page: 'Ranking' },
    { text: 'Utilizador', icon: 'icon/accon.svg', page: 'User' },
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
      background-color: #1f6807;;
      padding: 10px;

    }
  
    .menu-item {
      display: flex;
      align-items: center;
      margin-bottom: 8px;
      background-color: #1f6807;
    }
  
    .icon {
      margin-right: 8px;
    }
  </style>
  
  <div class="menu">
    {#each menuItems as item}
      <a class="menu-item" href="" on:click={handleClick} data-page={item.page}>
        <img src={item.icon} alt={item.link} />
        <span>{item.text}</span>
      </a>
    {/each}
  </div>