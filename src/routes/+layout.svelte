<script>
    import "../app.css";
    import {LoggedInState, logOut} from '../utils/auth.js'
    //import {logOut} from '../utils/auth.js'

  </script>
<!-- implement top nav bar -->

<nav class='navbar'>
  <div class="container mx-auto flex flex-row-reverse items-center flex-wrap-reverse sm:flex-nowrap">
    {#if $LoggedInState}
      <button class="bg-black hover:bg-gray-900 text-white font-bold py-2 px-4 rounded ml-3" on:click={logOut}>
        Logout
      </button>
      {:else}
      <button class="bg-black hover:bg-gray-900 text-white font-bold py-2 px-4 rounded ml-3" on:click={() => {window.location.href = '/login'}}>Login</button>
    {/if}
<!-- hide button when logged in -->
    <button class="bg-black hover:bg-gray-900 text-white font-bold py-2 px-4 rounded ml-3" on:click={() => {window.location.href = '/jobs/new'}}>
      Post A Job
    </button>
  </div>
</nav>


<style>
  .navbar{
     display: flex;
     flex-direction: row;
     align-items: right;
     position: absolute;
  }
 </style>

  <slot />