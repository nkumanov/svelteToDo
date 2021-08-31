<script>
    async function getData() {
		let response = await fetch(
			"https://jsonplaceholder.typicode.com/todos"
		);

		let data = await response.json();
		if (response.ok) {
			return Object.values(data).slice(0, 10);
		} else {
			throw new Error(data);
		}
	}
    
</script>

<section class="toDoItems">
    <p><strong>Tasks to do today:</strong></p>
    {#await getData()}
        <p>... loading</p>
    {:then items}
        {#each items as item}
            <div id = {item.id} on:click>
                <span>Task Number - {item.id}</span>
                <p><strong>Task:</strong> {item.title}</p>
            </div>
        {/each}
    {:catch error}
        <p>{error.message}</p>
    {/await}
</section>

<style> 
.toDoItems {
		display: flex;
		justify-content: center;
		flex-direction: column;
		border: 1px solid black;
		padding: 25px;
		border-radius: 15px;
	}

	.toDoItems div {
		border: 1px solid rgb(180, 177, 177);
		padding: 10px;
		margin-bottom: 5px;
		border-radius: 20px;
		cursor: pointer;
	}
	.toDoItems div span {
		font-weight: bold;
	}
</style>
