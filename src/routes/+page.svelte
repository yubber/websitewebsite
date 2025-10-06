<script>
	import SpinText from "$lib/components/SpinText.svelte";
	import GlitchText from "$lib/components/GlitchText.svelte";
	import SlideshowContainer from "$lib/components/SlideshowContainer.svelte";

	let projectsItems = ["code", "videos", "misc"];
	let webtoysItems = ["crappy ui", "games", "misc"];
</script>

<SlideshowContainer brightness={20}>
	<div class="crt h-dvh overflow-hidden flex flex-col">
		<div class="h-full flex place-content-center justify-center flex-col">
			<SpinText class="stretchroman text-[10rem] text-blue-700">yubz' website</SpinText>

			<div class="flex place-items-center items-start font-mono text-gray-100 lowercase justify-around w-full text-2xl">
				<div>
					<!-- maybe enable peer hover + -->
					<GlitchText class="peer" data_text="projects"></GlitchText>
					<div class="text-m dropdownContainer glow">
						{#each projectsItems as item, i}
							<a href="/projects/{item}" class="dropdownItem" style="transition-delay: {i * 0.05}s">
								{item}
							</a>
						{/each}
					</div>
				</div>
				<GlitchText class="hovergrow" href="/ramblings" data_text="ramblings"></GlitchText>
				<GlitchText class="hovergrow" href="/shrines" data_text="shrines"></GlitchText>
				<div>
					<!-- maybe enable peer hover + -->
					<GlitchText class="peer" data_text="webtoys"></GlitchText>
					<div class="text-m dropdownContainer glow">
						{#each webtoysItems as item, i}
							<a href="/webtoys/{item}" class="dropdownItem" style="transition-delay: {i * 0.05}s">
								{item}
							</a>
						{/each}
					</div>
				</div>
				<GlitchText class="hovergrow" href="/about" data_text="about"></GlitchText>
			</div>
		</div>
		<div class="text-center text-gray-100 text-sm text-shadow-lg">
			&copy; 2025 yubz (ys) | this site contains no ai generated assets. all media belongs to their respective owners. you are not allowed to train ai models on this site's content. | <a class="underline" href="https://github.com/yubber/websitewebsite">open source</a>
		</div>
	</div>
</SlideshowContainer>

<style>
	@import 'tailwindcss';
</style>