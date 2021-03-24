<script context="module">
  import { default as DNS } from "dat-dns";
  let peerPiperWellKnown = DNS({
    recordName: "doug/piper",
    hashRegex: /^[0-9a-f]{64}?$/i,
    protocolRegex: /^piper:\/\/([0-9a-f]{64})/i,
    txtRegex: /^"?piper=([0-9a-f]{64})"?$/i,
  });

  export async function preload(page, session) {
    try {
      const wellKnown = await peerPiperWellKnown.resolveName(
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
  import SchemaComp from "./schema.svelte";

  export let wellKnown;
  // Check if there's a ./.well-known/dat to load data
  // if not, load the hypercreator
  onMount(async () => {
    if (!wellKnown) {
      try {
        wellKnown = await peerPiperWellKnown.resolveName(
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
<main>
  <h1>Great success!</h1>

  <p>Well-Known: {wellKnown}</p>

  <strong>
    Created with Sapper. Edit this file (src/routes/index.svelte) to, well,
    edit.
  </strong>
  <p>Demos:</p>
  <ul>
    <li><a href="/schema" rel="external">Schema.org Explorer</a></li>
  </ul>
</main>

<style>
  h1,
  p {
    text-align: left;
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
  main {
    padding: 12px;
  }
  /* .container {
    width: 50%;
    height: 550px;
    overflow-y: auto;
    padding: 0.5em;
    margin: 0.5em;
    border: 5px solid rgba(128, 128, 128, 0.486);
    border-radius: 8px;
  } */
</style>
