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

<select name="" id="selectItem">
    <option value="">&#8212;</option>
    {#await getData()}
        <p>... loading</p>
    {:then items}
        {#each items as item}
            <option value={item.id}>Task : {item.id}</option>
        {/each}
    {:catch error}
        <p>{error.message}</p>
    {/await}
</select>

<style> 

</style>
