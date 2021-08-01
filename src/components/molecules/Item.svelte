<script lang="ts">
    import { createEventDispatcher } from 'svelte';
    import { quintOut } from 'svelte/easing';
    import { fly  } from 'svelte/transition';
    import Checkbox from '../atoms/Checkbox.svelte';

    const dispatch = createEventDispatcher();
    export let id;
    export let text;
    export let done;
    
    function toggleDone() {
        dispatch('toggleDone', { id });
    }
</script>

<div
    transition:fly="{{delay: 100, duration: 300, x: 0, y: 20, easing: quintOut}}"
    >
    <label class:done={done} for={id}>
        <Checkbox on:change={toggleDone} bind:checked={done} {id}></Checkbox>
        {text}
    </label>
</div>

<style>
    label {
        cursor: pointer;
    }
    .done {
        color: #999;
        text-decoration: line-through;
    }
</style>