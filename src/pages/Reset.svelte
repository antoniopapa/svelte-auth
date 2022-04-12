<script lang="ts">
    import axios from 'axios';
    import {push} from 'svelte-spa-router';

    let password = '', password_confirm = '';

    export let params;

    $: submit = async () => {
        await axios.post('reset', {
            token: params.token,
            password,
            password_confirm
        });

        await push('/login');
    }
</script>

<main class="form-signin">
    <form on:submit|preventDefault={submit}>
        <h1 class="h3 mb-3 fw-normal">Please reset your password</h1>

        <div class="form-floating">
            <input bind:value={password} type="password" class="form-control" placeholder="Password">
            <label>Password</label>
        </div>

        <div class="form-floating">
            <input bind:value={password_confirm} type="password" class="form-control" placeholder="Password Confirm">
            <label>Password Confirm</label>
        </div>

        <button class="w-100 btn btn-lg btn-primary" type="submit">Submit</button>
    </form>
</main>
