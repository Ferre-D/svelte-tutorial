<script>
	
	import {setContext, onMount, afterUpdate} from "svelte"
	//components
	import Navbar from "./components/Navbar.svelte";
	import ExpensesList from "./components/ExpensesList.svelte";
	import Totals from "./components/Totals.svelte"
	import ExpenseForm from "./components/ExpenseForm.svelte";
	import Modal from "./components/Modal.svelte";
	//Data
	import expensesData from "./expenses"
	//variables
	let expenses = [];
	//Set editing variables
	let setName ="";
	let setAmount = null;
	let setID = null;
	//toggle form variables
	let isFormOpen = false;
	//reactive
	$:isEditing = setID ?true:false;
	$:total = expenses.reduce((acc, curr) =>{
		return acc+curr.amount
	},0)
	//functions
	function showForm(){
		isFormOpen = true;
	}
	function hideForm(){
		isFormOpen = false;
		setName = "";
		setAmount = null;
		setID = null;
	}
	function removeExpense(id){
		expenses = expenses.filter(e => e.id !== id);
	}
	function clearExpenses(){
		expenses = [];
	}
	function addExpense({name, amount}){
        let expense = {
			id: Math.random() * Date.now(),
			name,
			amount
		}
		expenses = [expense, ...expenses];
    }
	function setModifiedExpense(id){
		let expense = expenses.find(e => e.id == id);
		setID = expense.id;
		setName = expense.name;
		setAmount = expense.amount;
		showForm();
	}
	function editExpense({name, amount}){
		expenses = expenses.map(e => {
			return e.id === setID? {...e, name, amount}: {...e}
		})
		setID = null;
		setAmount = null;
		setName = "";
	}
	setContext("clearExpenses", clearExpenses)
	setContext("removeExpense", removeExpense)
	setContext("modifyExpense", setModifiedExpense)
	//local storage
	function setLocalStorage(){
		localStorage.setItem("expenses", JSON.stringify(expenses))
	}
	onMount(() => {
		expenses = localStorage.getItem("expenses") ?
		 JSON.parse(localStorage.getItem("expenses")): [];
	})
	afterUpdate(() => {
		setLocalStorage();
	})
</script>

<Navbar {showForm}/>
<main class="content">
{#if isFormOpen}
	<Modal><ExpenseForm {addExpense} {hideForm} {editExpense}
		 {isEditing} name={setName} amount={setAmount}/></Modal>
	{/if}
	<Totals title="Total expenses" {total}/>
<ExpensesList {expenses}/>
</main>


