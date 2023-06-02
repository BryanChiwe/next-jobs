<script>
    import { authenticateUser } from "../../utils/auth";
    import { goto } from '$app/navigation';
    let formErrors = {};

  
    async function LoggedIn(evt) {
      evt.preventDefault();
  
      const userData = {
        username: evt.target['username'].value,
        password: evt.target['password'].value
      };

      const res = await authenticateUser(userData.username, userData.password)
  
        if (res.success) {
          goto('/');
        } 
    }
</script>


  <div class="text-center">
    <h1 class="text-center text-xl"> Login </h1>
    <a class="link-hover italic text-xs" href="/users/new">Don't have an account? Create an account now</a>
  </div>
<div class="flex justify-center items-center mt-8">
    <form on:submit={LoggedIn} class="w-1/3">
        <div class="form-control w-full">
            <label class="label" for="username">
                <span class="label-text">Username</span>
            </label>
            <input type="text" name="username" placeholder="johndoe" class="input input-bordered w-full" />
            {#if 'username' in formErrors}
            <label class="label" for="username">
                <span class="label-text-alt text-red-500">{formErrors['username'].message}</span>
            </label>
            {/if}
        </div>

        <div class="form-control w-full">
            <label class="label" for="password">
                <span class="label-text">Password</span>
            </label>
            <input type="password" name="password" placeholder="password" class="input input-bordered w-full" required />
            {#if 'password' in formErrors}
            <label class="label" for="password">
                <span class="label-text-alt text-red-500">{formErrors['password'].message}</span>
            </label>
            {/if}
        </div>

        <div class="form-control w-full mt-4">
            <button class="btn btn-md">Login</button>
        </div>
    </form>
</div>

