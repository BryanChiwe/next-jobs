<script>
    import "../app.css";
    import {LoggedInState} from '../utils/auth.js'
    import {logOut} from '../utils/auth.js'
  </script>
<!-- implement top nav bar -->

<nav class='navbar'>
  <div class="container mx-auto flex flex-row-reverse items-center flex-wrap-reverse sm:flex-nowrap">
    {#if $LoggedInState}
      <button class="bg-black hover:bg-gray-900 text-white font-bold py-2 px-4 rounded ml-3">
        Logout
      </button>
      {:else}
      <button class="bg-black hover:bg-gray-900 text-white font-bold py-2 px-4 rounded ml-3">Login</button>
    {/if}

    <button class="bg-black hover:bg-gray-900 text-white font-bold py-2 px-4 rounded ml-3" href="/users/new">
      Home
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