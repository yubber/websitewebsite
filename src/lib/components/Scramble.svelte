<script>
	let {len=4} = $props();
	var garble = $state('');
	$effect(() => {
		const interval = setInterval(() => {
			garble = (Math.random() + 1).toString(36).substring(2, len+2)
		}, 30);
		return () => clearInterval(interval); // Cleanup
	});
</script>

<span class="mono">
	{garble}
	<!-- {#each garble as letter (letter)}
		<span class="mono">
			{letter}
		</span>
	{/each} -->
</span>

<style>
	span.mono {
		/* display: inline-block; */
		font-family: 'Courier New', Courier, monospace;
		font-kerning: none;
		font-feature-settings: "liga" 0;
	}
</style>

