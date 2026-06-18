<script>
	import Banner from "$lib/components/Banner.svelte";
</script>

<div class="w-64">
{#each [...Array(10).keys()] as i (i)}
	<Banner design={i}>

	</Banner>
{/each}
</div>