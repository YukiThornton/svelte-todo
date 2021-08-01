<script lang="ts">
    export let disabled;
</script>

<button on:click {disabled}>
    <slot></slot>
</button>

<style>
    button {
        cursor: pointer;
        border: none;
        background-color: rgb(43, 172, 204);
        color: rgb(230, 244, 248);
        border-radius: 5px;
        padding: 7px 20px;
    }
    
    button:hover {
        background-color: rgb(61, 184, 214);
    }
    
    button:disabled {
        cursor: not-allowed;
        background-color: rgb(135, 158, 163);
        color: rgb(235, 232, 232);
    }
</style>