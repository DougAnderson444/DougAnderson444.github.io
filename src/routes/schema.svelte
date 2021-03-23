<script>
    import { onMount } from "svelte";

    let SchemaComponent, mounted;

    onMount(() => {
        import(
            /* webpackChunkName: "schema-explorer-comp" */ "schema-explorer"
        ).then((module) => {
            SchemaComponent = module.default;
            mounted = true;
        });
    });

    $: mounted && SchemaComponent ? open() : null;
</script>

{#if SchemaComponent}
    <svelte:component this={SchemaComponent} />
{/if}
