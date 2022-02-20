
<script>
    import {slide} from "svelte/transition"
    import {getContext} from "svelte"
    export let name ="";
    export let amount =0;
    export let id;

    let displayAmount = false;
    const removeExpense = getContext("removeExpense");
    const setModifyExpense = getContext("modifyExpense");
</script>

<article class="single-expense">
    <div class="expense-info">
        <h2>{name} 
            <button on:click={() => displayAmount = !displayAmount}
                 class="amount-btn">
            <i class="fas fa-caret-down"></i>
        </button></h2>
        {#if displayAmount}
        <h4 transition:slide>Amount: €{amount}</h4>
        {/if}
    </div>
    <div class="expense-buttons">
        <button class="expense-btn edit-btn" on:click={() => {setModifyExpense(id)}}>
            <i class="fas fa-pen"></i>
        </button>
        <button on:click={() => {removeExpense(id)}} 
            class="expense-btn delete-btn">
            <i class="fas fa-trash"></i>
        </button>
    </div>
</article>

