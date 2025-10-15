<script>
	import SpinText from "$lib/components/SpinText.svelte";
	import SlideshowContainer from "$lib/components/SlideshowContainer.svelte";
	import "$lib/winxp.css";
</script>

<SlideshowContainer slides={
	[{url: 'https://frutigeraeroarchive.org/images/wallpapers/asadal_stock/asadal_stock_71.jpg', styles:'bg-cover'}]}>

	<div class="window m-12 h-[90svh]">
		<div class="title-bar">
			<div class="title-bar-text">My Code Projects !!!</div>
			<div class="title-bar-controls">
				<button class="xp" aria-label="Minimize"></button>
				<button class="xp" aria-label="Maximize"></button>
				<a href="/"><button class="xp" aria-label="Close"></button></a>
			</div>
		</div>
		<div class="window-body flex flex-col justify-around">
			<SpinText class="font-mono text-9xl text-green-400" lumDrop={0.01}>code</SpinText>

			<div class="flex flex-row justify-evenly justify-items-center mt-6 content-stretch">
				<div class="flex-0 flex place-items-center">
					<button class="xp">games</button>
				</div>
				<div class="flex-0 flex justify-around place-items-center">
					<button class="retrobtn m-0">tools</button>
				</div>
				<div class="flex-0 flex place-items-center content-stretch">
					<div class="metal p-1 rounded-full w-full h-full">
						<button class="dlbtn px-2 py-1 rounded-full">test</button>
					</div>
				</div>
			</div>
		</div>
	</div>
</SlideshowContainer>

<style>
	.title-bar {
		height: auto;
	}

	.retrobtn {
		box-sizing: content-box;
		border: solid 3px transparent;
		height: 2.5em;
		padding: 0 1.75em;
		border-radius: 1em;
		box-shadow: inset 0 0 0 3px rgba(255, 255, 255, 0.2), inset 0 -1.25em 1.25em -1.25em #494b4f;
		--ini: circle farthest-side at;
		--lst: 0, transparent 100%, #383d41;
		--set: bottom 1.25em/ 0.625em 0.625em no-repeat padding-box;
		background: radial-gradient(var(--ini) 100% var(--lst)) left 0 var(--set), radial-gradient(var(--ini) 0 var(--lst)) right 0 var(--set), linear-gradient(#64686a, #45494d 50%, #383d41 0) padding-box, linear-gradient(#2e3034, #1e2024) border-box;
		/* color: #e9eae9; */
		font: inherit;
		color: whitesmoke;
		text-shadow: 1px 1px #434343, 1px 1px 3px #323232;
		&:active {
			filter: brightness(0.5);
			box-shadow: inset 0 0 0 3px rgba(255, 255, 255, 0.849), inset 0 -1.25em 1.25em -1.25em #494b4f;
			/* border-top: 1px; */
			/* background: radial-gradient(var(--lst) 100% var(--ini)) left 0 var(--set), radial-gradient(var(--lst) 0 var(--ini)) right 0 var(--set), linear-gradient(#64686a, #45494d 50%, #383d41 0) padding-box, linear-gradient(#2e3034, #1e2024) border-box; */
		}
	}

	.dlbtn {
		width: 100%;
		height: 100%;
		background: linear-gradient(
			var(--color-green-700) 0%,
			var(--color-green-200) 100%
		)
	}

	.metal {
		background: linear-gradient(
			135deg,
			#999 5%,
			#fff 10%,
			#ccc 30%,
			#ddd 50%,
			#ccc 70%,
			#fff 80%,
			#999 95%
		);
	}
</style>