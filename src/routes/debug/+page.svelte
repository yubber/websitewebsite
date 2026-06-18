<script>
	import Banner from "$lib/components/Banner.svelte";
</script>

<div class="lg:w-72">
{#each [...Array(20).keys()] as i (i)}
	<Banner design={i}>

	</Banner>
{/each}
</div>