<script lang="ts">
    import { createEventDispatcher } from 'svelte';
    export let value;
    
    const dispatch = createEventDispatcher();
    
    function handleKeypress(e: KeyboardEvent) {
        if (e.key === 'Enter') { 
            dispatch('inputFinished', {
                value
            });
            value = ''
        }
    }
</script>

<input bind:value on:keypress={handleKeypress}/>