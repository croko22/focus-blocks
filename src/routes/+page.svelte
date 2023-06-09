<script>
	import Timer from '$lib/components/Timer.svelte';

	let block = {
		name: '',
		time: 0
	}

	let savedBlock = JSON.parse(localStorage.getItem('block') || '{}');

	const saveToLocal = () => {
		localStorage.setItem('block', JSON.stringify(block));
		savedBlock = JSON.parse(localStorage.getItem('block') || '{}');
	}
</script>

<div class="container h-full mx-auto flex justify-evenly items-center">
	<div class="space-y-5">
		<h1 class="h1">Focus blocks</h1>
		<input class="bg-transparent rounded-md" type="text" placeholder="Focus block name" bind:value={block.name}>
		<input class="bg-transparent rounded-md" type="number" placeholder="25" bind:value={block.time}>
		<button class="btn variant-filled rounded-md" on:click={saveToLocal}>Save block</button>		
		
		<!-- * Saved blocks -->
		<div class="space-y-5">
			<h1 class="h1">Saved block</h1>
			<p>{savedBlock.name}</p>
			<p>{savedBlock.time}</p>
		</div>
	</div>



	<Timer />
</div>
