<script>
	const designCount = 9
	let {design = Math.round(Math.random() * (designCount-1))} = $props()
</script>

{#if design === 1}
<div class="grey3d pixelFont flex items-center justify-around">
	<img src="https://media.tenor.com/kRXFmZ-gciEAAAAj/aol-aol-guy.gif" alt="">
	This user is dancing!
</div>
{:else if design === 2}
<div class="window">
		<div class="title-bar">
			<div class="title-bar-text">Alert</div>
			<div class="title-bar-controls">
				<button class="xp" aria-label="Minimize"></button>
				<button class="xp" aria-label="Maximize"></button>
				<a href="/"><button class="xp" aria-label="Close"></button></a>
			</div>
		</div>
		<div>
			Your computer loves you!
		</div>
	</div>
{/if}

<style>
	.grey3d {
		border: outset 2px white;
	}
</style>