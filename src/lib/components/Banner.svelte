<script>
	const designCount = 9
	let {design = Math.round(Math.random() * (designCount-1))} = $props()

	import heartgif from "$lib/assets/heart.gif"
	import warninggif from "$lib/assets/warning.gif"
	import youradhere from "$lib/assets/youradhere.gif"
	import snuff562 from "$lib/assets/4562-snuff.png"
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
			<button class="xp">OK</button>
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
			<img src={warninggif} alt="">
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
		Deleting C:\Windows\system32...
		<progress class="xp"></progress>
	</div>
</div>
{:else if design === 5}
<div class="bg-blue-50">
	<h2 class="text-center font-bold">
		DO IT APPLICATION
	</h2>
	<hr>
	<ol>
		<li>
			<label>
				What are your prospects?
				<input type="text" placeholder="Type your response here">
			</label>
		</li>
		<li>
			Do you make your own cash?<br>
			<label>
				<input type="radio">
				Yes
			</label><br>
			<label>
				<input type="radio">
				No
			</label>

		</li>
		<li>
			Do you like rough ***?<br>
			<label>
				<input type="radio">
				Yes
			</label><br>
			<label>
				<input type="radio">
				No
			</label>
		</li>
		<li>
			<label>
				What kinda car you drive?
				<input type="text" placeholder="Type your response here">
			</label>
		</li>
	</ol>
</div>
{:else if design === 6}
<img src={youradhere} alt="" width="100%">
{:else if design === 7}
<img src={snuff562} alt="" width="100%">
{:else if design === 8}
<div class="flex flex-col justify-center">
	<h2>FL STUDIO FREE DOWNLOAD</h2>
	<SpinText class="text-9xl">
		🥕
	</SpinText>
	<button class="dlbtn">
		<svg xmlns="http://www.w3.org/2000/svg" width="100" height="100" viewBox="0 0 24 24" fill="none" stroke="#000000" stroke-width="1" stroke-linecap="butt" stroke-linejoin="arcs"><path d="M3 15v4c0 1.1.9 2 2 2h14a2 2 0 0 0 2-2v-4M17 9l-5 5-5-5M12 12.8V2.5"/></svg>
		DOWNLOAD NOW
	</button>
</div>
{:else if design === 9}
<div class="text-4xl flashing impact text-center">
	HOT GIRLS
</div>
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
</style>