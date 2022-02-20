<script>
    // your script goes here
    import {onMount, onDestroy, beforeUpdate, afterUpdate} from "svelte";
    // onMount(() => {
    //     console.log("form has mounted");
    // })
    // onDestroy(() => {
    //     console.log("on destroy")
    // })
    // beforeUpdate(() => {
    //     console.log("before update");
    // })
    // afterUpdate(() => {
    //     console.log("after update")
    // })
    
    import Title from "./Title.svelte"
    export let addExpense;
    export let name ="";
    export let amount = null;
    export let isEditing;
    export let editExpense;
    export let hideForm;
    //variables
    $: isEmpty = !name || !amount
    function handleSubmit(){
        if(isEditing){
            editExpense({name, amount})
        }
        else{
            addExpense({name, amount})
        }
        name ="";
        amount = null;
        hideForm();
    }
</script>

<style>
    /* your styles go here */
</style>
<section class="form">
<Title title="Add expense"/>
<form class="expense-form" on:submit|preventDefault={handleSubmit}>
    <div class="form-control">
        <label for="name">name</label>
        <input type="text" bind:value={name} id="name">
    </div>
    <div class="form-control">
        <label for="amount">amount</label>
        <input type="number" bind:value={amount} id="amount">
    </div>
    {#if isEmpty}
         <p class="form-empty">Please fillout all form fields</p>
    {/if}
        <button disabled={isEmpty} class:disabled={isEmpty}
         type="submit" class="btn btn-block">
             {isEditing ? "Edit expense" : "Add expense"}
        </button>
    <button type="button" class="close-btn" on:click={hideForm}>
        <i class="fas fa-times"></i> Close
    </button>
</form>
</section>

