<script lang="ts">
    export let checked;
    export let id;
</script>

<input type="checkbox" on:change bind:checked={checked} {id} />

<style>
    input {
        cursor: pointer;
    }
</style>