<script>
    // https://www.nielsvandermolen.com/new-architecture-svelte-api-platform/
    let email = '';
    let password = '';
    export let handleSubmit = async function(event) {
        console.log('submit');
        console.log(email);
        console.log(password);
        console.log(event);
        // Call an authenication microservice to handle the authentication.
        const response = await fetch("http://localhost:8001/api/",
        {
            // TODO: test
            method: 'POST',
            headers: {
                'Accept': 'application/json',
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({email: email, password: password})
        });
        // TODO: store in session persisted with Redis either using Store or a library
        // E.g. express-session
    };
</script>

<form on:submit|preventDefault="{handleSubmit}">
  <label for="email">Email:</label>
  <input type="email" id="email" bind:value={email} required />
  <label for="password">Password:</label>
  <input type="password" id="password" bind:value={password} required />
  <button type="submit">Account aanmaken</button>
</form>