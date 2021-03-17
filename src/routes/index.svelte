<script context="module">
  import { default as DNS } from "dat-dns";
  let datDns = DNS();

  export async function preload() {
    try {
      const wellKnown = await datDns.resolveName(
        "https://douganderson444.github.io/"
      );
      return { wellKnown };
    } catch (error) {
      console.error(error);
      return { wellKnown: false };
    }
  }
</script>

<script>
  import { onMount } from "svelte";

  export let wellKnown;
  console.log({ wellKnown });
  // Check if there's a ./.well-known/dat to load data
  // if not, load the hypercreator
  onMount(async () => {
    if (!wellKnown) {
      try {
        wellKnown = await datDns.resolveName(
          "https://douganderson444.github.io/"
        );
      } catch (error) {
        console.error(error);
      }
    }
  });
</script>

<svelte:head>
  <title>Doug's Github Page</title>
</svelte:head>

<h1>Great success!</h1>

<p>Well-Known: {wellKnown}</p>

<p>
  <strong>
    Created with Sapper. Edit this file (src/routes/index.svelte) to, well,
    edit.
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
