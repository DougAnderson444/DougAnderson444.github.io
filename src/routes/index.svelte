<script context="module">
  export async function preload() {
    const res = await this.fetch(`/.well-known/dat`);
    const wellKnown = await res.text();
    return { wellKnown };
  }
</script>

<script>
  import { onMount } from "svelte";

  export let wellKnown;

  // Check if there's a ./.well-known/dat to load data
  // if not, load the hypercreator
  onMount(async () => {
    const res = await fetch("/.well-known/dat");
    //wellKnown = await res.text();
  });
</script>

<svelte:head>
  <title>Doug's Github Page</title>
</svelte:head>

<h1>Great success!</h1>

<p>Well-Known: {wellKnown}</p>

<p>
  <strong>
    Editing this file (src/routes/index.svelte) to test live reloading.
  </strong>
</p>

<style>
  h1,
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

  p {
    margin: 1em auto;
  }

  @media (min-width: 480px) {
    h1 {
      font-size: 4em;
    }
  }
</style>
