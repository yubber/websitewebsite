<script>
	import SlideshowContainer from "$lib/components/SlideshowContainer.svelte";
	import FacingText3D from "$lib/components/FacingText3D.svelte";
	import SpinText from "$lib/components/SpinText.svelte";
	let titles = ["shrines"]
</script>

<container>
	<div class="text-7xl my-auto mx-auto fixed top-1/2 left-1/2 z-0 translate-x-[-50%]">
		<FacingText3D layers={12} gapPx={2} class="font-sans scale-x-150 scale-y-250 text-pink-900">
			shrines
		</FacingText3D>
	</div>
	<div class="relative text-center mt-[50dvh] font-mono z-10 text-lg text-BodyColor">
		A shrine is a page on a personal website, dedicated to the author's favorite things.
	</div>

	<div id="floaty-container" class="flex flex-row justify-around items-end align-middle text-BodyColor z-0 sticky top-0 mb-[49dvh] p-4">
		<div id="music-floaty">
			<SpinText layers={4} gapPx={1}>
				<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path fill="currentColor" d="M22 .847V17a4 4 0 1 1-2-3.465V3.153L8 4.867V19a4 4 0 1 1-2-3.465V3.133z"/></svg>
			</SpinText>
			<span class="section-float-title-normal">
				music
			</span>
			<div class="section-float-title-animated">
				<FacingText3D layers=12 gapPx=2>
					music
				</FacingText3D>
			</div>
		</div>
		<div id="games-floaty">
			<SpinText layers={4} gapPx={1}>
				<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path fill="currentColor" d="M21.94 3H2.06L.937 21H7.72l1-3h6.558l1 3h6.785zM11 9.5v2H9v2H7v-2H5v-2h2v-2h2v2zm5-2h2.004v2.004H16zm2.004 3.996V13.5H16v-2.004z"/></svg>
			</SpinText>
			<span class="section-float-title-normal">
				games
			</span>
			<div class="section-float-title-animated">
				<FacingText3D layers=12 gapPx=2>
					games
				</FacingText3D>
			</div>
		</div>
		<div id="shows-floaty">
			<SpinText layers={4} gapPx={1}>
				<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path fill="currentColor" d="M15.5 10H18v3l5-2.477v10.954L18 19v3H1V10h1.55a3.5 3.5 0 1 1 5.025-4.87A5.001 5.001 0 1 1 15.501 10M8.29 8.698A3.5 3.5 0 0 1 7.45 10H9.5a5 5 0 0 1-1.21-1.302"/></svg>
			</SpinText>
			<span class="section-float-title-normal">
				shows
			</span>
			<div class="section-float-title-animated">
				<FacingText3D layers=12 gapPx=2>
					shows
				</FacingText3D>
			</div>
		</div>
		<div>
			<SpinText layers={4} gapPx={1}>
				<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path fill="currentColor" d="M7.48 2.58L1 .66v12.053h.007C1.222 18.458 6.091 23 12 23s10.778-4.542 10.993-10.286H23V.661L16.52 2.58A11.2 11.2 0 0 0 12 1.639c-1.609 0-3.14.336-4.52.94M5.137 3.972A11 11 0 0 0 3 6.177V3.34zM21 3.339v2.838a11 11 0 0 0-2.137-2.205zM9 12H7V9h2zm8 0h-2V9h2zm-4.105 2.053c.378.757.856.985 1.188 1.013c.34.028.759-.131 1.085-.62l.555-.833l1.664 1.11l-.555.832c-.674 1.01-1.755 1.6-2.915 1.504c-.713-.06-1.37-.37-1.917-.885c-.546.515-1.204.826-1.917.885c-1.16.097-2.241-.494-2.915-1.504l-.555-.832l1.664-1.11l.555.832c.326.49.745.65 1.085.621c.332-.028.81-.256 1.189-1.013l.894-1.79z"/></svg>
			</SpinText>
			<span class="section-float-title-normal">
				pets
			</span>
			<div class="section-float-title-animated">
				<FacingText3D layers=12 gapPx=2>
					pets
				</FacingText3D>
			</div>
		</div>
	</div>
	<div>
		<div class="h-dvh flex flex-row" id="music">
			<div class="parallax bg-[url(https://wallpaperaccess.com/full/259517.jpg)] h-full flex-1">
			</div>
			<div class="flex-3">

			</div>
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
	container {
		timeline-scope: --musicScroll;
	}

	#music {
		view-timeline-name: --musicScroll;
		/* view-timeline: --musicScroll y; */
	}

	#music-floaty {
		@media not (prefers-reduced-motion) {
			.section-float-title-animated {
				animation-name: to-title;
				animation-timeline: --musicScroll;
				transition: all;
				animation-fill-mode: forwards;
				animation-timing-function: ease-in;
				animation-range: exit;
			}
		}
	}

	@keyframes fadeout {
		from {
			opacity: 1;
		}
		to {
			opacity: 0;
		}
	}

	@keyframes to-title {
		from {
			translate: 0 0;
			scale: 100% 100%;
			color: var(--color-BodyColor);
		}
		to {
			translate: 50vw -50vh;
			scale: 150% 250%;
			color: var(--color-pink-900);
		}
	}

	.parallax {
		background-attachment: fixed;
		background-position: center;
		background-repeat: no-repeat;
		background-size: cover;
	}
</style>