<script lang="ts">
	import Timer from '$lib/components/Timer.svelte';
	import {browser} from '$app/environment';
	import Block from '$lib/components/Block.svelte';

	let block = {
		name: '',
		time: 0
	} 

	let savedBlock = JSON.parse(browser && localStorage.getItem('block') || '{}');

	const saveToLocal = () => {
		browser && localStorage?.setItem('block', JSON.stringify(block));
		savedBlock = JSON.parse(browser && localStorage.getItem('block') || '{}');
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
			<h1 class="h1">Saved blocks</h1>
			<div class="block bg-yellow-500 rounded-md p-4 text-black">
				<p>{savedBlock.name}</p>
				<p>{savedBlock.time}</p>
			</div>
			<Block name={savedBlock.name} time={savedBlock.time} />
		</div>
	</div>



	<Timer />
</div>

<style>
	.block {
		width: 100%;
		height: var(--block-height, 100px); /* Default height */
		transition: height 0.3s ease;
	}
</style>