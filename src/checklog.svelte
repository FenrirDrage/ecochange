<script>
  import { onMount } from 'svelte';
  import { signInWithEmailAndPassword, signOut, auth } from 'firebase/auth';

  let isLoggedIn = false;

  onMount(() => {
    // Check if the user is already logged in
    const unsubscribe = auth.onAuthStateChanged((user) => {
      isLoggedIn = user ? true : false;
    });

    return () => {
      unsubscribe();
    };
  });

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

{#if isLoggedIn}
  <p>User is logged in</p>
{:else}
  <p>User is not logged in</p>
{/if}

<div>
  <label for="email">Email:</label>
  <input type="email" id="email" />
</div>
<div>
  <label for="password">Password:</label>
  <input type="password" id="password" />
</div>
<button on:click={logIn}>Log In</button>
<button on:click={logOut}>Log Out</button>
