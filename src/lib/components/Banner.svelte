<script>
	const designCount = 16
	let {design = Math.round(Math.random() * (designCount-1))} = $props()

	import heartgif from "$lib/assets/heart.gif"
	import cakegif from "$lib/assets/cake.gif"
	import warninggif from "$lib/assets/warning.gif"
	import youradhere from "$lib/assets/youradhere.gif"
	import snuff562 from "$lib/assets/4562-snuff.png"
	import advquest from "$lib/assets/advquest.png"
	import highputergif from "$lib/assets/highputer.gif"
	import eyezlogo from "$lib/assets/eyezmaze_logo.png"
	import eyez1 from "$lib/assets/m_GROW_CUBE_OMEGA.png"
	import eyez2 from "$lib/assets/m_GROW_RECOVERY.png"
	import eyez3 from "$lib/assets/m_GROW_v1.png"
	import eyez4 from "$lib/assets/m_GROW_valley.png"
	import eyez5 from "$lib/assets/m_tontirulin.png"
	import "$lib/winxp.css";
	import SpinText from "./SpinText.svelte";
	// import "$lib/test.css";
</script>

{#if design === 1}
<div class="grey3d pixelFont flex items-center justify-around bg-gray-400">
	<img src="https://media.tenor.com/kRXFmZ-gciEAAAAj/aol-aol-guy.gif" alt="" class="max-w-[30%]">
	This user is dancing!
</div>
{:else if design === 2}
<div class="xp-window">
	<div class="title-bar">
		<div class="title-bar-text">Alert</div>
		<div class="title-bar-controls">
			<button class="xp" aria-label="Minimize"></button>
			<button class="xp" aria-label="Maximize"></button>
			<button class="xp" aria-label="Close"></button>
		</div>
	</div>
	<div class="p-2">
		<div class="flex items-center gap-4 p-4">
			<img src={heartgif} alt="">
			<span>
				Your computer loves you!
			</span>
		</div>
		<section class="field-row justify-end pt-4">
			<button class="xp">OK</button>
			<button class="xp">yay &lt;3</button>
		</section>
	</div>
</div>
{:else if design === 9}
<div class="xp-window">
	<div class="title-bar">
		<div class="title-bar-text">Unfortunately, the clock is ticking</div>
		<div class="title-bar-controls">
			<button class="xp" aria-label="Close"></button>
		</div>
	</div>
	<div class="p-2">
		<div class="flex items-center gap-4 p-4">
			<img src={cakegif} alt="">
			<span>
				the hours are going by. The past increases, the future recedes. Possibilities decreasing, regrets mounting.
				<br>Do you understand?
			</span>
		</div>
		<section class="field-row justify-end pt-4">
			<button class="xp">I Understand</button>
			<button class="xp">remain ignorant</button>
		</section>
	</div>
</div>
{:else if design === 3}
<div class="xp-window">
	<div class="title-bar">
		<div class="title-bar-text">Alert</div>
		<div class="title-bar-controls">
			<button class="xp" aria-label="Close"></button>
		</div>
	</div>
	<div class="p-2">
		<div class="flex items-center gap-4 p-4">
			<img src={warninggif} alt="" width="20%">
			<span>
				Look behind you
			</span>
		</div>
		<section class="field-row justify-end pt-4">
			<button class="xp">OK</button>
			<button class="xp">Cancel</button>
		</section>
	</div>
</div>
{:else if design === 4}
<div class="xp-window">
	<div class="title-bar">
		<div class="title-bar-text">Death</div>
	</div>
	<div class="p-4">
		Deleting C:\Windows\system32...<br>
		<progress class="xp"></progress>
	</div>
</div>
{:else if design === 5}
<div class="bg-blue-50">
	<h2 class="text-center font-bold">
		DO IT APPLICATION
	</h2>
	<hr>
	<ol class="list-decimal p-2 pl-8">
		<li class="py-1">
			<label>
				What are your prospects?
				<input type="text" placeholder="Type your response here" class="border-b-1 border-black">
			</label>
		</li>
		<li class="py-1">
			Do you make your own cash?<br>
			<label>
				<input type="radio" name="owncash">
				Yes
			</label><br>
			<label>
				<input type="radio" name="owncash">
				No
			</label>

		</li>
		<li class="py-1">
			Do you like rough ***?<br>
			<label>
				<input type="radio" name="roughsex">
				Yes
			</label><br>
			<label>
				<input type="radio" name="roughsex">
				No
			</label>
		</li>
		<li class="py-1">
			<label>
				What kinda car you drive?
				<input type="text" placeholder="Type your response here" class="border-b-1 border-black">
			</label>
		</li>
	</ol>
	<div class="w-full flex justify-around p-2">
		<a href="https://www.youtube.com/watch?v=Zd0j0xnhWFw">DO IT</a>
	</div>
</div>
{:else if design === 6}
<img src={youradhere} alt="" width="100%">
{:else if design === 7}
<a href="https://www.4562.world/sick-13">
	<img src={snuff562} alt="" width="100%">
</a>
{:else if design === 8}
<div class="flex flex-col justify-center bg-blue-950 text-red-50">
	<h2>FL STUDIO FREE DOWNLOAD</h2>
	<SpinText class="text-9xl">
		🥕
	</SpinText>
	<button class="dlbtn">
		<svg xmlns="http://www.w3.org/2000/svg" width="100" height="100" viewBox="0 0 24 24" fill="none" stroke="#000000" stroke-width="1" stroke-linecap="butt" stroke-linejoin="arcs"><path d="M3 15v4c0 1.1.9 2 2 2h14a2 2 0 0 0 2-2v-4M17 9l-5 5-5-5M12 12.8V2.5"/></svg>
		CLICK NOW
	</button>
</div>
{:else if design === 10}
<div class="text-4xl flashing impact text-center">
	HOT GIRLS<br>
	CLICK HERE
</div>
{:else if design === 11}
<div class="text-4xl impact text-center overflow-clip bg-red-500 text-white">
	<div class="marquee text-nowrap">
		i want that poplife walk right talk nice
	</div>
</div>
{:else if design === 12}
<div class="flex flex-col justify-center">
	stopsign

	YOUR MIND IS INFECTED
	<button>
		Scan now
	</button>
</div>
{:else if design === 13}
<div>
	SpinText
	CONGRATULATIONS! YOU ARE A WINNER!
	CLAIM YOUR FREE ESCAPE FROM SAMSARA
</div>
{:else if design === 14}
<div>
	Meet Single Horses in Your City
</div>
{:else if design === 15}
<img src={advquest} alt="" width="100%">
{:else if design === 0}
<a href="https://www.eyezmaze.com/">
	<div class="grid grid-cols-3 justify-items-center">
		{#each [eyezlogo, eyez1, eyez2, eyez3, eyez4, eyez5] as pic, i (i)}
			<img src={pic} alt="">
		{/each}
	</div>
</a>
{/if}

<style>
	.grey3d {
		border: outset 6px white;
	}

	.impact {
		font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
	}

	.flashing {
		animation: 0.1s infinite flashing;
		@media (prefers-reduced-motion: reduce) {
			animation: 5s infinite flashing;
		}
	}

	.marquee {
		animation: 5s infinite scroll-left linear;
		@media (prefers-reduced-motion: reduce) {
			animation: 7s infinite flashing;
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

	@keyframes flashing {
		0% {
			background-color: white;
			color: black;
		}
		100% {
			background-color: black;
			color: white;
		}
	}

	@keyframes scroll-left {
		0% {
			translate: 100%;
		}
		100% {
			translate: -200%;
		}
	}
</style>