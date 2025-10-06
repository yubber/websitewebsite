<script>
	import SpinText from "$lib/components/SpinText.svelte";
	import SlideshowContainer from "$lib/components/SlideshowContainer.svelte";
</script>

<SlideshowContainer slides={
	[{url: 'https://frutigeraeroarchive.org/images/wallpapers/asadal_stock/thumbnails/asadal_stock_71.jpg', styles:''}]}>
	<SpinText class="stretchroman text-9xl" lumDrop={0.01}>code</SpinText>
</SlideshowContainer>
<div class="w-6xl flex flex-col justify-around m-auto">
	<button class="retrobutton"> test </button>
</div>