
<script>
    import {fly} from "svelte/transition"
    import {flip} from "svelte/animate"

    import Title from "./Title.svelte"
    import ExpenseItem from "./ExpenseItem.svelte";
    import ClearExpenses from "./ClearExpenses.svelte";

    export let expenses = [];
</script>
<style>
    h2{
        text-transform: capitalize;
    }
</style>
<section>
<Title title="Expense List"/>
{#each expenses as expense, index (expense.id)}
<div transition:fly={{x:200, delay:index*300}} animate:flip>
    <ExpenseItem {...expense}/>

</div>
{:else}
     <h2>No expenses added yet</h2>
{/each}
{#if expenses.length > 0}
<ClearExpenses/>
{/if}
</section>

