<script>
	import firecvnt from "$lib/assets/stickers/firecvnt.gif"
	import ilmc from "$lib/assets/stickers/ilmc8831.png"
	import opensource from "$lib/assets/stickers/open source.gif"

	import SpinText from "$lib/components/SpinText.svelte";
	import GlitchText from "$lib/components/GlitchText.svelte";
	import MouseDots from "$lib/components/MouseDots.svelte";
    import { onMount } from "svelte";

	let fonti = 0
	let fontSwitch
	let fonts = ["'Times New Roman MT Condensed', Times, serif", "Courier New", "Arial", "Comic Sans MS"]
	let projectsItems = ["code", "videos", "misc"]
	let webtoysItems = ["crappy ui", "games", "misc"]

	onMount(() => {
		setInterval(() => {
			fonti++
			fonti %= fonts.length
			fontSwitch = fonts[fonti]
		}, 400)
	})
</script>

<MouseDots></MouseDots>

<div class="h-dvh overflow-hidden flex flex-col darkxpbg">
	<div class="h-full flex place-content-center justify-center flex-col">
		<div class="stretchroman">
			<SpinText class="text-[10rem] text-blue-700">yubz' website</SpinText>
		</div>

		<div class="flex place-items-center items-start font-mono text-gray-100 lowercase justify-around w-full text-2xl"
			style="--fontSwitch: {fontSwitch}"
			>
			<div>
				<!-- maybe enable peer hover + -->
				<GlitchText class="peer" data_text="projects"></GlitchText>
				<div class="text-m dropdownContainer glow">
					{#each projectsItems as item, i (i)}
						<a href="/projects/{item}" class="dropdownItem" style="transition-delay: {i * 0.05}s">
							{item}
						</a>
					{/each}
				</div>
			</div>
			<GlitchText class="hovergrow" href="/shrines" data_text="shrines"></GlitchText>
			<div>
				<!-- maybe enable peer hover + -->
				<GlitchText class="peer" data_text="webtoys"></GlitchText>
				<div class="text-m dropdownContainer glow">
					{#each webtoysItems as item, i (i)}
						<a href="/webtoys/{item}" class="dropdownItem" style="transition-delay: {i * 0.05}s">
							{item}
						</a>
					{/each}
				</div>
			</div>
			<GlitchText class="hovergrow" href="/about" data_text="about"></GlitchText>
		</div>
	</div>
	<div class="text-center text-gray-100 text-sm text-shadow-lg h-[31px] inline-flex flex-row justify-center z-0 gap-2 mb-1">
		<span class="h-full">
			<img src={firecvnt} alt="Firefox Now!">
		</span>
		<a href="https://www.youtube.com/watch?v=RKybAhTw8iE&list=PLQQj6Cezh2Nupac5mjljKE-SncM_2Go59&index=5" class="h-full">
			<img src={ilmc} alt="Ninajirachi - I Love My Computer" class="h-full object-contain">
		</a>
		<a href="https://github.com/yubber/websitewebsite" class="">
			<img src={opensource} alt="open source">
		</a>
	</div>
</div>

<style>
	@import 'tailwindcss';
	.darkxpbg {
		background:
        	/* top, transparent black, faked with gradient */
			linear-gradient(
				rgba(0, 0, 0, 0.55),
				rgba(0, 0, 0, 0.55)
			),
			/* bottom, image */
			url("https://frutigeraeroarchive.org/images/wallpapers/windows_xp/windows_xp_16.jpg");
    }

	.peer:hover {
		font-family: var(--fontSwitch);
	}
</style>