<script>
  import { onMount, setContext } from "svelte";
  import {
    key as userContextKey,
    initialValue as userContextInitialValue
  } from "../userContext";
  import LoginForm from "./LoginForm.svelte";
  onMount(() => {
    setContext(userContextKey, userContextInitialValue);
  });
  const submit = ({ email, password }) =>
    new Promise((resolve, reject) => {
      setTimeout(() => {
        setContext(userContextKey, {
          name: "Foo",
          lastName: "Bar",
          email: "foo@bar.com"
        });
        resolve();
      }, 1000);
    });
</script>

<style>
  h1,
  figure,
  p {
    text-align: center;
    margin: 0 auto;
  }

  h1 {
    font-size: 2.8em;
    text-transform: uppercase;
    font-weight: 700;
    margin: 0 0 0.5em 0;
  }

  figure {
    margin: 0 0 1em 0;
  }

  img {
    width: 100%;
    max-width: 400px;
    margin: 0 0 1em 0;
  }

  p {
    margin: 1em auto;
  }

  @media (min-width: 480px) {
    h1 {
      font-size: 4em;
    }
  }
  section {
    height: 100vh;
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    background: linear-gradient(to right, #cd76e2, #e358ab);
  }
</style>

<svelte:head>
  <title>Sapper project template</title>
</svelte:head>

<h1>Great success!</h1>

<figure>
  <img alt="Borat" src="great-success.png" />
  <figcaption>HIGH FIVE!</figcaption>
</figure>

<p>
  <strong>
    Try editing this file (src/routes/index.svelte) to test live reloading.
  </strong>
</p>

<section>
  <LoginForm {submit} />
</section>
