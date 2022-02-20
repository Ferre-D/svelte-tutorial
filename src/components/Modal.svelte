<script>
    import {blur, fade, fly} from "svelte/transition";
</script>

<style>
    /* your styles go here */
</style>

<div class="modal-container" in:blur out:fade>
    <div class="modal-content" transition:fly={{y:200}}>
        <slot></slot>
    </div>
</div>