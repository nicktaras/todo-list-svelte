<script>
	let newItem = "";

	// Example todo:
	// { text: "Write my first post", status: true }
	let todoList = localStorage.getItem("todos")
		? JSON.parse(localStorage.getItem("todos"))
		: [];

	function addToList() {
		todoList = [...todoList, { text: newItem, status: false }];
		newItem = "";
		localStorage.setItem("todos", JSON.stringify(todoList));
	}

	function removeFromList(index) {
		todoList.splice(index, 1);
		todoList = todoList;
		localStorage.setItem("todos", JSON.stringify(todoList));
	}

	function changeStatus(index) {
		todoList[index].status = !todoList[index].status;
		localStorage.setItem("todos", JSON.stringify(todoList));
	}
</script>

<style>
	.checked {
		text-decoration: line-through;
	}
</style>

<form on:submit|preventDefault={addToList}>
	<input bind:value={newItem} type="text" placeholder="new todo item.." />
	<button type="submit"> Submit </button>
</form>

{#each todoList as item, index}
	<input
		on:click={() => changeStatus(index)}
		bind:checked={item.status}
		type="checkbox" />
	<span class:checked={item.status}>{item.text}</span>
	<span style="cursor: pointer" on:click={() => removeFromList(index)}>🗑</span>
	<br />
{/each}
