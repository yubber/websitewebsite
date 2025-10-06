<script>
	import SlideshowContainer from "$lib/components/SlideshowContainer.svelte";
	import FacingText3D from "$lib/components/FacingText3D.svelte";
    import Text3D from "$lib/components/Text3D.svelte";
</script>

<div class="h-dvh align-middle flex flex-col justify-around">
		<div class="text-7xl my-auto mx-auto absolute top-1/2 left-1/2 blur-[1px] brightness-50">
			<FacingText3D RGB={[138,206,0]} layers={16} gapPx={1} lumDrop={0.03} class="font-sans scale-y-400">
				shrines
			</FacingText3D>
		</div>
	<div class="flex-0 text-center my-auto font-mono z-0">
		A shrine is a page on a personal website, dedicated to the author's favorite things.
	</div>
</div>
<div class="h-dvh flex flex-row">
	<div class="parallax bg-[url(https://wallpaperaccess.com/full/259517.jpg)] h-full flex-1">
	</div>
	<div class="flex-3">

	</div>
</div>

<style>
	.parallax {
		background-attachment: fixed;
		background-position: center;
		background-repeat: no-repeat;
		background-size: cover;
	}
</style>