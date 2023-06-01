<script>
    import { LoggedInState, authenticateUser } from "../../utils/auth";
    import { onMount } from 'svelte';

    let username = '';
    let password = '';
    let formErrors = {}

    async function handleLogin() {
        const LoggedIn = await authenticateUser(username, password);
        if (LoggedIn.success) {
            localStorage.setItem('token', LoggedIn.res.token);
            window.location.href = '/homepage';
        } else {
            if (LoggedIn.res.reason === 'email_not_found') {
                alert('Email does not exist. Please create an account.');
            } else if (LoggedIn.res.reason === 'invalid_password') {
                alert('Invalid password. Please try again.');
            } else {
                alert('Login failed. Please try again.');
            }
        }
    }

    onMount(() => {
        LoggedInState.subscribe((value) => {
            if (value) {
                isLoggedIn = true;
            }
        });
    });
  </script>

  <h1 class="text-center text-xl"> Login </h1>
  <div class="text-center">
    <a class="link-hover italic text-xs" href="/users/new">Don't have an account? Create an account now</a>
</div>
<div class="flex justify-center items-center mt-8">
    <form on:submit|preventDefault={handleLogin} class="w-1/3">
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
            <input type="password" name="password" placeholder="" class="input input-bordered w-full" required />
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

