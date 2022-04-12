<script>
    import axios from "axios";
    import {authenticated} from "../../store/auth";
    import {push} from "svelte-spa-router";

    export let loginData = {};
    let code = '';

    $: submit = async () => {
        const {data} = await axios.post('two-factor', {
            ...loginData,
            code
        }, {withCredentials: true});

        axios.defaults.headers.common['Authorization'] = `Bearer ${data.token}`;

        authenticated.set(true);

        await push('/');
    }
</script>

<form on:submit|preventDefault={submit}>
    <h1 class="h3 mb-3 fw-normal">Please insert your authenticator code</h1>

    <div class="form-floating">
        <input bind:value={code} class="form-control" placeholder="6 digits code">
        <label>6 digits code</label>
    </div>

    <button class="w-100 btn btn-lg btn-primary mt-3" type="submit">Submit</button>
</form>
