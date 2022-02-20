<script>
    import {getContext} from "svelte"

    let clearExpenses = getContext("clearExpenses")
</script>

<style>
    /* your styles go here */
</style>
<button type="button" class="btn btn-primary btn-block"
on:click={clearExpenses}>
 Clear expenses
</button>
<!-- markup (zero or more items) goes here -->