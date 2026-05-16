<script>
	import firecvnt from "$lib/assets/stickers/firecvnt.gif"
	import ilmc from "$lib/assets/stickers/ilmc8831.png"
	import opensource from "$lib/assets/stickers/open source.gif"

	import SpinText from "$lib/components/SpinText.svelte";
	import GlitchText from "$lib/components/GlitchText.svelte";
	import MouseDots from "$lib/components/MouseDots.svelte";
    import { onMount } from "svelte";

	let items = [{
		"name": "projects",
		"dropdown": ["code", "videos", "misc"]
	},{
		"name": "shrines",
		dropdown: ["music", "other media", "pets"]
	},{
		"name": "webtoys",
		"dropdown": ["crappy ui", "games", "misc"]
	},{
		"name": "about"
	}]
</script>

<MouseDots></MouseDots>

<div class="h-dvh flex flex-col darkxpbg">
	<div class="h-full flex place-content-center justify-center flex-col">
		<div class="stretchroman">
			<SpinText class="text-[10rem] text-blue-700 cursor-default">yubz' website</SpinText>
		</div>

		<div class="flex place-items-center items-start font-mono text-gray-100 lowercase justify-around w-full text-2xl">
			{#each items as item, i (i)}
				<div>
					<GlitchText class="hoverfont{item.dropdown ? ' peer cursor-default' : ''}" data_text={item.name} href="{item.dropdown ? null : item.name}">
					</GlitchText>
					{#if item.dropdown}
						<div class="text-m dropdownContainer glow">
							{#each item.dropdown as d, j (j)}
								<a href="/{item.name}/{d}" class="dropdownItem" style="transition-delay: {j * 0.05}s">
									{d}
								</a>
							{/each}
						</div>
					{/if}
				</div>
			{/each}
		</div>
	</div>
	<div class="text-center text-gray-100 text-sm text-shadow-lg h-[31px] inline-flex flex-row justify-center z-0 gap-2 mb-1">
		<span class="h-full">
			<img src={firecvnt} alt="Firefox Now!">
		</span>
		<a href="https://www.youtube.com/watch?v=RKybAhTw8iE&list=PLQQj6Cezh2Nupac5mjljKE-SncM_2Go59&index=5" class="h-full">
			<img src={ilmc} alt="Ninajirachi - I Love My Computer" class="h-full object-contain outset">
		</a>
		<a href="https://github.com/yubber/websitewebsite" class="">
			<img src={opensource} alt="open source">
		</a>
	</div>
</div>

<style>
	@import 'tailwindcss';
	.outset {
		border: outset 2px white;
	}

	.darkxpbg {
		background-size: cover;
		background:
        	/* top, transparent black, faked with gradient */
			linear-gradient(
				rgba(0, 0, 0, 0.55),
				rgba(0, 0, 0, 0.55)
			),
			/* bottom, image */
			url("https://frutigeraeroarchive.org/images/wallpapers/windows_xp/windows_xp_16.jpg");
    }

	.hoverfont :hover{
		animation: hoverfont 1s infinite step-end;
	}

	@keyframes hoverfont {
		0% {
			font-family: 'Times New Roman MT Condensed', Times, serif;
		}
		33% {
			font-family: 'Courier New', Courier, monospace;
			letter-spacing: 0.1em;
		}
		66% {
			font-family: 'Arial Narrow', Arial, Helvetica, sans-serif;
			letter-spacing: normal;
		}
	}


</style>