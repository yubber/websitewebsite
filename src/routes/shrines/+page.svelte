<script>
	import SlideshowContainer from "$lib/components/SlideshowContainer.svelte";
	import FacingText3D from "$lib/components/FacingText3D.svelte";
	import SpinText from "$lib/components/SpinText.svelte";
	import Album from "./Album.svelte";

	import CandyFilter from "$lib/components/CandyFilter.svelte";

	import pop2 from "$lib/assets/pop2.png"
	let titles = ["shrines"]
</script>

<container>
	<div class="text-7xl fixed top-[-1em] left-[-1em] max-h-lvh w-lvw wrap-break-word">
		{#each Array(20) as _, i}
			<div class="scale-x-150 scale-y-250 translate-x-[25%] translate-y-[-75%]">
				<FacingText3D layers={6} gapPx={4} scalar={0.015} class="font-sans text-pink-800">
					shrines
				</FacingText3D>
			</div>
		{/each}
	</div>
	<div class="relative text-center mt-[50dvh] font-mono z-10 text-lg text-BodyColor">
		A shrine is a page on a personal website, dedicated to the author's favorite things.
	</div>

	<div id="floaty-container" class="flex flex-row justify-around items-end align-middle text-BodyColor z-0 sticky top-0 mb-[49dvh] p-4">
		<div id="music-floaty">
			<SpinText layers={4} gapPx={1}>
				<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path fill="currentColor" d="M22 .847V17a4 4 0 1 1-2-3.465V3.153L8 4.867V19a4 4 0 1 1-2-3.465V3.133z"/></svg>
			</SpinText>
			<span class="section-float-title-normal font-mono">
				music
			</span>
		</div>
		<div id="games-floaty">
			<SpinText layers={4} gapPx={1}>
				<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path fill="currentColor" d="M21.94 3H2.06L.937 21H7.72l1-3h6.558l1 3h6.785zM11 9.5v2H9v2H7v-2H5v-2h2v-2h2v2zm5-2h2.004v2.004H16zm2.004 3.996V13.5H16v-2.004z"/></svg>
			</SpinText>
			<span class="section-float-title-normal font-mono">
				games
			</span>
		</div>
		<div id="shows-floaty">
			<SpinText layers={4} gapPx={1}>
				<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path fill="currentColor" d="M15.5 10H18v3l5-2.477v10.954L18 19v3H1V10h1.55a3.5 3.5 0 1 1 5.025-4.87A5.001 5.001 0 1 1 15.501 10M8.29 8.698A3.5 3.5 0 0 1 7.45 10H9.5a5 5 0 0 1-1.21-1.302"/></svg>
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
	</div>
	<div>
		<div class="h-lvh" id="music">
			<div class="grid grid-flow-row grid-cols-4 z-0 mx-auto p-8">
				<Album title="Pop 2" artist="Charli XCX" year="2017" img="https://ucsdguardian.org/wp-content/uploads/2018/01/Pop-2-ALBUM-COVER.jpg" class="bg-[#c9a1dd]">
					<CandyFilter animateDuration={5}/>
					<div class="h-full w-full" mask="url(#candy)">
						<SpinText brightnessDrop={0}>
							<img src={pop2} alt="">
						</SpinText>
					</div>
					<p class="p-4">
						NOBODY DOES IT LIKE HER!!! everything about this album feels like it's from some utopian future, from the visuals to the sound design. this album is stuffed full of bangers, though some of the rap parts can feel a bit out of place. i guess it's punishment for leaking xcx world.
					</p>
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
	</div>
</container>

<style>
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