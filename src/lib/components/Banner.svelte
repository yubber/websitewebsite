<script>
	const designCount = 9
	let {design = Math.round(Math.random() * (designCount-1))} = $props()
</script>

{#if design === 1}
<div>

</div>
{:else if design === 2}

{/if}

<style>
	.grey3d {
		border: outset 2px white;
	}
</style>