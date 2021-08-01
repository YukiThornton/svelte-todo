<script lang="ts">
    import Item from './../molecules/Item.svelte'
    export let items
    export let color = "#cbd0d4";
    export let emptyMessage = '';
</script>

<article>
    <header>
        <div><slot name="title" class="title"></slot></div>
        <div><slot name="action"></slot></div>
    </header>
    <section style="background-color: {color}">
        {#if items.length !== 0}
            {#each items as {id, text, done} (id)}
                <Item {id} {text} {done} on:toggleDone />
            {/each}
        {:else}
            <p>{emptyMessage}</p>
        {/if}
    </section>
</article>

<style>
    header {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        grid-template-areas: ". center right";
        justify-items: center;
        align-items: center;
    }
    
    header > :nth-child(1) {
        grid-area: center;
    }
    
    header > :nth-child(2) {
        grid-area: right;
    }
    
    section {
        padding: 5%;
        border-radius: 20px;
    }
</style>