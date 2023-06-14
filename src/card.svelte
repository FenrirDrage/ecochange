<script>
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();
  
    function handleAddCard() {
      // Dispatch an event to indicate that the "Adicionar Cartão" button was clicked
      dispatch('addCard');
    }
  </script>
  
  <a href="" class="menu-link" on:click={handleAddCard}>
    <div class="card">
      <h1>+</h1>
      <h2>Adicionar Cartão</h2>
    </div>
  </a>