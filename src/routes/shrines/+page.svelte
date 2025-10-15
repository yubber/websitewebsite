<script>
	import SlideshowContainer from "$lib/components/SlideshowContainer.svelte";
	import FacingText3D from "$lib/components/FacingText3D.svelte";
	import SpinText from "$lib/components/SpinText.svelte";
	import Album from "./Album.svelte";

	import CandyFilter from "$lib/components/CandyFilter.svelte";

	import pop2 from "$lib/assets/pop2.png"
	import ninaface from "$lib/assets/smileyfaceblue.png"
	let titles = ["shrines"]
</script>

<container>
	<div class="text-7xl fixed top-1/2 left-1/2 max-h-lvh w-lvw wrap-break-word">
		<div class="scale-x-150 scale-y-250 translate-x-[-50%] translate-y-[-50%] w-fit">
			<FacingText3D layers={6} gapPx={4} scalar={0.015} class="font-sans text-pink-800">
				shrines
			</FacingText3D>
		</div>
	</div>
	<div class="relative text-center mt-[50dvh] font-mono z-10 text-lg text-BodyColor">
		A shrine is a page on a personal website, dedicated to the author's favorite things.
	</div>

	<div id="floaty-container" class="flex flex-row justify-around items-end align-middle text-BodyColor z-10 sticky top-0 mb-[49dvh] p-4">
		<div id="music-floaty">
			<SpinText layers={4} gapPx={1}>
				<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><g fill="none" fill-rule="evenodd"><path d="m12.593 23.258l-.011.002l-.071.035l-.02.004l-.014-.004l-.071-.035q-.016-.005-.024.005l-.004.01l-.017.428l.005.02l.01.013l.104.074l.015.004l.012-.004l.104-.074l.012-.016l.004-.017l-.017-.427q-.004-.016-.017-.018m.265-.113l-.013.002l-.185.093l-.01.01l-.003.011l.018.43l.005.012l.008.007l.201.093q.019.005.029-.008l.004-.014l-.034-.614q-.005-.018-.02-.022m-.715.002a.02.02 0 0 0-.027.006l-.006.014l-.034.614q.001.018.017.024l.015-.002l.201-.093l.01-.008l.004-.011l.017-.43l-.003-.012l-.01-.01z"/><path fill="currentColor" d="M18.671 3.208A2 2 0 0 1 21 5.18V17a4 4 0 1 1-2-3.465V9.18L9 10.847V18q0 .09-.015.174A3.5 3.5 0 1 1 7 15.337v-8.49a2 2 0 0 1 1.671-1.973zM9 8.82l10-1.667V5.18L9 6.847z"/></g></svg>
			</SpinText>
			<span class="section-float-title-normal font-mono">
				music
			</span>
		</div>
		<div id="games-floaty">
			<SpinText layers={4} gapPx={1}>
				<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><g fill="none"><path d="m12.593 23.258l-.011.002l-.071.035l-.02.004l-.014-.004l-.071-.035q-.016-.005-.024.005l-.004.01l-.017.428l.005.02l.01.013l.104.074l.015.004l.012-.004l.104-.074l.012-.016l.004-.017l-.017-.427q-.004-.016-.017-.018m.265-.113l-.013.002l-.185.093l-.01.01l-.003.011l.018.43l.005.012l.008.007l.201.093q.019.005.029-.008l.004-.014l-.034-.614q-.005-.018-.02-.022m-.715.002a.02.02 0 0 0-.027.006l-.006.014l-.034.614q.001.018.017.024l.015-.002l.201-.093l.01-.008l.004-.011l.017-.43l-.003-.012l-.01-.01z"/><path fill="currentColor" d="M17 4c1.106 0 1.955.843 2.584 1.75l.213.321l.195.32q.093.157.178.308c.787 1.407 1.472 3.244 1.925 5.059c.45 1.801.699 3.682.54 5.161C22.475 18.404 21.71 20 20 20c-1.534 0-2.743-.82-3.725-1.621l-1.11-.931C14.242 16.692 13.232 16 12 16s-2.243.692-3.164 1.448l-1.11.93C6.742 19.18 5.533 20 4 20c-1.711 0-2.476-1.596-2.635-3.081c-.158-1.48.09-3.36.54-5.161c.453-1.815 1.138-3.652 1.925-5.059l.178-.309l.195-.319l.213-.321C5.045 4.843 5.894 4 7 4c.51 0 1.017.124 1.515.27l.593.182q.147.045.292.086c.865.248 1.75.462 2.6.462s1.735-.214 2.6-.462l.885-.267C15.983 4.124 16.49 4 17 4M8.5 8a2.5 2.5 0 1 0 0 5a2.5 2.5 0 0 0 0-5m7 0a1 1 0 0 0-1 1v.5H14a1 1 0 1 0 0 2h.5v.5a1 1 0 1 0 2 0v-.5h.5a1 1 0 1 0 0-2h-.5V9a1 1 0 0 0-1-1m-7 2a.5.5 0 1 1 0 1a.5.5 0 0 1 0-1"/></g></svg>
			</SpinText>
			<span class="section-float-title-normal font-mono">
				games
			</span>
		</div>
		<div id="shows-floaty">
			<SpinText layers={4} gapPx={1}>
				<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><g fill="none" fill-rule="evenodd"><path d="m12.594 23.258l-.012.002l-.071.035l-.02.004l-.014-.004l-.071-.036q-.016-.004-.024.006l-.004.01l-.017.428l.005.02l.01.013l.104.074l.015.004l.012-.004l.104-.074l.012-.016l.004-.017l-.017-.427q-.004-.016-.016-.018m.264-.113l-.014.002l-.184.093l-.01.01l-.003.011l.018.43l.005.012l.008.008l.201.092q.019.005.029-.008l.004-.014l-.034-.614q-.005-.019-.02-.022m-.715.002a.02.02 0 0 0-.027.006l-.006.014l-.034.614q.001.018.017.024l.015-.002l.201-.093l.01-.008l.003-.011l.018-.43l-.003-.012l-.01-.01z"/><path fill="currentColor" d="M16 7a4 4 0 0 1-.554 2.033A3 3 0 0 1 18 12v.21l1.713-1.056A1.5 1.5 0 0 1 22 12.43v5.138a1.5 1.5 0 0 1-2.287 1.277L18 17.79V18a3 3 0 0 1-3 3H5a3 3 0 0 1-3-3v-6a3 3 0 0 1 1.545-2.624a3.5 3.5 0 0 1 5.138-4.612A4 4 0 0 1 16 7m-4-2a2 2 0 1 0 0 4a2 2 0 0 0 0-4M6.5 9a1.5 1.5 0 1 0 0-3a1.5 1.5 0 0 0 0 3"/></g></svg>
			</SpinText>
			<span class="section-float-title-normal font-mono">
				shows
			</span>
		</div>
		<div>
			<SpinText layers={4} gapPx={1}>
				<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path fill="currentColor" d="M7.48 2.58L1 .66v12.053h.007C1.222 18.458 6.091 23 12 23s10.778-4.542 10.993-10.286H23V.661L16.52 2.58A11.2 11.2 0 0 0 12 1.639c-1.609 0-3.14.336-4.52.94M5.137 3.972A11 11 0 0 0 3 6.177V3.34zM21 3.339v2.838a11 11 0 0 0-2.137-2.205zM9 12H7V9h2zm8 0h-2V9h2zm-4.105 2.053c.378.757.856.985 1.188 1.013c.34.028.759-.131 1.085-.62l.555-.833l1.664 1.11l-.555.832c-.674 1.01-1.755 1.6-2.915 1.504c-.713-.06-1.37-.37-1.917-.885c-.546.515-1.204.826-1.917.885c-1.16.097-2.241-.494-2.915-1.504l-.555-.832l1.664-1.11l.555.832c.326.49.745.65 1.085.621c.332-.028.81-.256 1.189-1.013l.894-1.79z"/></svg>
			</SpinText>
			<span class="section-float-title-normal font-mono">
				pets
			</span>
		</div>
		<div>
			<SpinText layers={4} gapPx={1}>
				<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><g fill="none" fill-rule="evenodd"><path d="m12.594 23.258l-.012.002l-.071.035l-.02.004l-.014-.004l-.071-.036q-.016-.004-.024.006l-.004.01l-.017.428l.005.02l.01.013l.104.074l.015.004l.012-.004l.104-.074l.012-.016l.004-.017l-.017-.427q-.004-.016-.016-.018m.264-.113l-.014.002l-.184.093l-.01.01l-.003.011l.018.43l.005.012l.008.008l.201.092q.019.005.029-.008l.004-.014l-.034-.614q-.005-.019-.02-.022m-.715.002a.02.02 0 0 0-.027.006l-.006.014l-.034.614q.001.018.017.024l.015-.002l.201-.093l.01-.008l.003-.011l.018-.43l-.003-.012l-.01-.01z"/><path fill="currentColor" d="M11.41 2.017c.79.07 1.253.34 1.534.652c.343.381.556.983.556 1.831a1.5 1.5 0 0 1-2.27 1.288L11.1 5.7a1 1 0 1 0-1.2 1.6a3.5 3.5 0 0 0 5.6-2.8c0-.685-.102-1.369-.348-1.993C19.13 3.827 22 7.578 22 12c0 5.523-4.477 10-10 10S2 17.523 2 12c0-5.325 4.162-9.677 9.41-9.983m3.23 13.215a1 1 0 0 0-1.408.128c-.359.43-.798.64-1.232.64s-.873-.21-1.232-.64a1 1 0 0 0-1.536 1.28C9.904 17.447 10.876 18 12 18s2.096-.553 2.768-1.36a1 1 0 0 0-.128-1.408M8.5 10a1.5 1.5 0 1 0 0 3a1.5 1.5 0 0 0 0-3m7 0a1.5 1.5 0 1 0 0 3a1.5 1.5 0 0 0 0-3"/></g></svg>
			</SpinText>
			<span class="section-float-title-normal font-mono">
				childhood
			</span>
		</div>
	</div>
	<div>
		<div class="h-lvh" id="music">
			<div class="grid grid-flow-row grid-cols-4 z-0 mx-auto p-8 gap-4">
				<Album title="Pop 2" artist="Charli XCX" year="2017" img="https://ucsdguardian.org/wp-content/uploads/2018/01/Pop-2-ALBUM-COVER.jpg">
					{#snippet backImg()}
						<svg class="absolute w-full h-full z-0 overflow-clip" xmlns="http://www.w3.org/2000/svg">
							<filter id="candy" y='0%' width="100%" height="100%" opacity="0.2">
								<feTurbulence baseFrequency="0.011" stitchTiles="stitch"/>
								<!-- <animate attributeName="x" from="0%" to="100%" dur="5s" repeatCount="indefinite"/> -->
								<!-- <animate attributeName="baseFrequency" from="0.01" to="0.02" dur="5s" repeatCount="indefinite"/> -->
							</filter>
							<rect width="200%" height="100%" filter="url(#candy)"></rect>
						</svg>

						<div class="h-full w-full bg-[#f6ecff] p-4 flex justify-around items-center">
							<SpinText brightnessDrop={0} gapPx={1}>
								<img src={pop2} alt="pop 2 logo">
							</SpinText>
						</div>
					{/snippet}
					{#snippet slideout()}
						<p class="p-4 bg-[#c9a1dd] h-full overflow-scroll">
							NOBODY DOES IT LIKE HER!!! everything about this album feels like it's from some utopian future, from the visuals to the sound design. it's stuffed full of bangers, though some of the rap parts can feel a bit out of place. i guess it's punishment for leaking xcx world.
						</p>
					{/snippet}
				</Album>
				<Album title="I Love My Computer" artist="Ninajirachi" year="2025" img="https://f4.bcbits.com/img/a0649909828_10.jpg">
					{#snippet backImg()}
						<div class="w-full h-full bg-blue-300 p-4 flex justify-around items-center">
							<SpinText brightnessDrop={3} gapPx={1}>
								<img src={ninaface} alt="i love my computer icon">
							</SpinText>
						</div>
					{/snippet}
					{#snippet slideout()}
						<p class="p-4 stretchroman bg-gray-200 h-full overflow-scroll">
							This is the most perfect time capsule of how I experienced the internet growing up. Most people chasing the "y2k" aesthetic do it in a way that just isn't online enough, and it's hard to relate to because I was a child and also living nowhere near those subcultures. But Nina is so intimately familiar with the Internet at the time, and every little detail in this era just violently flings my brain down memory lane. As for the music itself, it feels like a more self-aware, less cheesy and more personal iteration of the EDM of that era. Which I was also a fan of as a kid. As a side note, I really appreciate her visionary use of Times New Roman.
						</p>
					{/snippet}
				</Album>
			</div>
		</div>
		<div id="shows">
			Serial experiments lain
			She's just like me fr. People have praised the show to the moon and back about how spot on it was in predicting the way we interact with technology today, but my favorite part of it is how it creates such an alienating, lonely atmosphere. There are long, uncomfortable stretches of silence and huge chunks of white space that really make you feel alone. Even in scenes where something dramatic happens (like the "everyone's connected" one and the explosion), the shots don't complement what's happening. It's just a slow, quiet view of those events happening before you that makes them feel almost unreal. I also think the way its horror elements use our own sense of shame is really interesting. In that way, the characters don't fear for their personal safety, but instead they worry about how other people treat them and judge them. Which is all too real.

			chiikawa
			I normally only enjoy this sort of hyper-cutesy franchise stuff in a half-ironic way because it feels too consumerist to get into it fully. But this show has a very childlike innocence and simplicity that makes me really sincerely enjoy it. I also really, really like watching those Chinese animations where the characters act in really stupid ways. <a href="https://www.instagram.com/nb666sb520/">This account is my favorite.</a> The animation quality is really good and it pioneered a lot of the trends that other creators copied, like 拉长耳朵 and making the characters cartoonishly jiggly.
		</div>
		<div id="pets" class="h-lvh text-BodyColor">
			yubber
			He was my first rabbit. We adopted him as a baby, from someone who neglected to spay their own rabbits. I was young when we had him, so there was a lot to be improved about how we cared for him. He normally doesn't like being touched, so my most treasured memory of him is when he weakly nudged my hand to ask for pets during his final days.

			bit bit
			My current rabbit. May he live long and happy. He's a total brat though. He's potty trained, but I swear he pees on the floor in front of me whenever he's angry for whatever reason. He loves being rubbed on the head, but will do everything in his power to avoid being picked up. It's impossible to stay mad at him though, he's practically engineered for maximum cuteness.
		</div>
		<div id="childhood" class="h-lvh text-BodyColor">
			https://www.eyezmaze.com/
		</div>
	</div>
</container>

<style>
	@import "tailwindcss";
	@source inline("overflow-hidden");

	#floaty-container {
		view-timeline-name: --navScroll;
		view-timeline-axis: block;

		/* Attach animation, linked to the  View Timeline */
		animation: linear bgFade forwards;
		animation-timeline: --navScroll;

		/* Tweak range when effect should run*/
		animation-range: contain 50% 90%;
	}

	@keyframes bgFade {
		from {
			background-color: rgba(0, 0, 0, 0);
		}
		to {
			background-color: rgba(3,7,18,1);
		}
	}

	.parallax {
		background-attachment: fixed;
		background-position: center;
		background-repeat: no-repeat;
		background-size: cover;
	}
</style>