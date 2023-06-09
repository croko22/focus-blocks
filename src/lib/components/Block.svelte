<script lang="ts">
	export let name = '';
	export let time = 0;

	let blockHeight = time / 10 + 'px'; // Adjust the multiplier as needed

	function updateTime(event) : void {
		time = parseInt(event.target.textContent);
        if (isNaN(time)) {
            time = 0;
        }
		blockHeight = `${time / 10}px`; // Adjust the multiplier as needed
	}
</script>

	<div class="block" style="--block-height: {blockHeight}">
		<p>{name}</p>
		<p contenteditable="true" class="time" on:input={updateTime} bind:textContent={time}>
			{time}
		</p>
	</div>

<style>
	.block {
		width: 100%;
		background-color: blue;
		height: var(--block-height, 100px); /* Default height */
		transition: height 0.3s ease;
	}
</style>
