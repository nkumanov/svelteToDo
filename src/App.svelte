<script>
	import ColorPicker from "./colorpicker.svelte";
	import ImportData from './importData.svelte'
	let color;
	let toggle = false;
	let selectedId = 0;

	const setColor = (event) => {
		color = event.detail;
	};

	function resolveCurrentTask() {
		let element = document.getElementById(`${selectedId}`)
		element.style.border = ''
		element.style.boxShadow = ''
		toggle = false
		selectedId = 0
	}
	function toggleColorPicker(){
		toggle = !toggle
	}
	function resolveAllTasks() {
		Array.from(document.querySelectorAll(".toDoItems div")).map(elem => {
			elem.style.border=''
			elem.style.boxShadow=''
			elem.style.background = `rgba(${color})`
		})
		toggle=false
	}
	function unresolveAllTasks(){
		Array.from(document.querySelectorAll(".toDoItems div")).map(elem => {
			elem.style.border=''
			elem.style.boxShadow=''
			elem.style.background = ``
		})
		toggle=false
	}

	function changeColorReactive() {
		if (selectedId != 0) {
			let item = document.getElementById(`${selectedId}`);
			item.style.background = `rgba(${color})`;
		}
	}
	function resolveSelectedItem(event){
		toggleColorPicker()
		if(event.target.id.match(/[0-9]+/)  || event.target.parentElement.id.match(/[0-9]+/)){
			let selectedItem = document.getElementById(`${event.target.id || event.target.parentElement.id}`)
			selectedId = selectedItem.id
			selectedItem.style.border = '2px solid red'
			selectedItem.style.boxShadow = '0px 0px 15px 14px rgba(0,0,0,0.2)'
		}
	}
	
</script>

<main>
	<section class="main-content">

		{#if toggle}
		<section class="container">
			<div id="colorPickField">
				<ColorPicker on:colorChange={setColor} on:colorChange={changeColorReactive} />
			</div>
			<button on:click={resolveCurrentTask}>Resolve selected task.</button>
			<button on:click={resolveAllTasks}>Mark all tasks as resolved.</button>
			<button on:click={unresolveAllTasks}>Mark all tasks as unresolved.</button>
		</section>
		{/if}
		<ImportData on:click={resolveSelectedItem}/>
	</section>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}
	.main-content {
		display: flex;
		justify-content: space-around;
	}
	#colorPickField {
		margin: 0 auto;
	}
	button{
		margin-top: 15px;
	}
	
	.container {
		display: flex;
		justify-content: flex-start;
		flex-direction: column;
	}
	
	
	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}

	@media screen and (max-width: 645px) {
		.main-content {
			flex-direction: column;
		}
	}
</style>
