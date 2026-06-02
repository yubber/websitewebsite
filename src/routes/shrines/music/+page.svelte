<script>
	import widgetblack from "$lib/assets/face+black+transparent.png"

	import { onMount } from "svelte";
	import { gsap } from "gsap";
	import { ScrollTrigger } from "gsap/ScrollTrigger";
	import { ScrollSmoother } from "gsap/all";
	import ScrambleTextPlugin from "gsap/ScrambleTextPlugin";

	import MovieMakerTitle from "$lib/components/MovieMakerTitle.svelte";
	import FacingText3D from "$lib/components/FacingText3D.svelte";
	import Text3D from "$lib/components/Text3D.svelte";

	let titleContainerOuter, titleContainerInner, albumTitle, particles, glitchOverlay, albumArtist
	let albumIndex = $state(0);
	let animating = $state();

	import widget from "$lib/assets/face+black+transparent.png";
	import house from "$lib/assets/house.png";

	onMount(()=>{
		gsap.registerPlugin(ScrollTrigger, ScrollSmoother, ScrambleTextPlugin);
		particles = Array.from(document.getElementsByClassName("particles"))

		ScrollSmoother.create({
			smooth: 0.3, // how long (in seconds) it takes to "catch up" to the native scroll position
			effects: true, // looks for data-speed and data-lag attributes on elements
			// smoothTouch: 0.1
		});

		let titleTl = gsap.timeline({
			scrollTrigger: {
				trigger: titleContainerOuter,
				start: "top top",
				end: "bottom top",
				scrub: 1,
				onLeave: () => {
					intentObserver.enable();
					albumIndex = 0
				},

				onEnterBack: () => {
					intentObserver.disable();
					albumIndex = 0
				}
			}
		})
		titleTl.fromTo(titleContainerInner, {rotateY: 0, scale: 1}, {rotateY: '360deg', scale: 0})
		gsap.set(glitchOverlay, {opacity: 0})

		// create an observer and disable it to start
		let intentObserver = ScrollTrigger.observe({
			type: "wheel,touch",
			onUp: () => !animating && albumIndex < albumData.length - 1 && changeAlbum(albumIndex + 1, true),
			onDown: () => !animating && albumIndex >= 0 && changeAlbum(albumIndex - 1, false),
			wheelSpeed: -1,
			tolerance: 10,
			preventDefault: true,
			onPress: (self) => {
				// on touch devices like iOS, if we want to prevent scrolling, we must call preventDefault() on the touchstart (Observer doesn't do that because that would also prevent side-scrolling which is undesirable in most cases)
				ScrollTrigger.isTouch && self.event.preventDefault();
			}
		});
		intentObserver.disable();

		function changeAlbum(index, isScrollingDown) {
			animating = true;
			// return to normal scroll if we're at the end or back up to the start
			if (
				(index === albumData.length && isScrollingDown) ||
				(index === -1 && !isScrollingDown)
			) {
				animating = false;
				intentObserver.disable();
				return;
			}

			gsap.fromTo(particles,
				{rotateY: 0 + 180 * (albumIndex % 2)},
				{rotateY: 90 + 180 * (albumIndex % 2),
				duration: 0.375,
				ease: "power1.in",
				onComplete: () => {
					albumIndex = index
				}
			})
			gsap.to(particles, {
				rotateY: 180 * (albumIndex % 2 + 1),
				duration: 0.375,
				delay: 0.375,
				ease: "back.out",
				onComplete: () => {
					animating = false
				}
			})

			gsap.to(glitchOverlay, {
				opacity: "100%",
				duration: 0.375,
			})
			gsap.fromTo(glitchOverlay,{
				opacity: "100%"
			},{
				opacity: "0%",
				duration: 0.37,
				delay: 0.38
			})

			gsap.to(albumTitle, {
				scrambleText: albumData[index].name,
				chars: 'upperAndLowerCase',
				duration: 0.5
			})
			gsap.to(albumArtist, {
				scrambleText: albumData[index].artist,
				chars: 'upperAndLowerCase',
				duration: 0.5
			})

		}

		// pin swipe section and initiate observer
		ScrollTrigger.create({
			trigger: ".swipe-section",
			pin: true,
			start: "top top",
			end: "+=1",
			onEnter: (self) => {
			},
			onEnterBack: () => {
				intentObserver.enable();
				albumIndex = albumData.length-1
				changeAlbum(albumIndex - 1, false);
			}
		});

	})

	let albumData = [{
		name: "I Love My Computer",
		artist: "Ninajirachi",
		cover: "https://upload.wikimedia.org/wikipedia/en/d/dd/I_Love_My_Computer_by_Ninajirachi.png",
		particles: widget,
		desc: ""
	},{
		name: "how i'm feeling now",
		artist: "Charli xcx",
		cover: "https://upload.wikimedia.org/wikipedia/en/b/bd/Charli_XCX_-_How_I%27m_Feeling_Now.png",
		particles: house
	},{
		name: "WOMB",
		artist: "Purity Ring",
		cover: "https://upload.wikimedia.org/wikipedia/en/c/c0/Purity_Ring_-_Womb.png"
	}]
</script>
<!-- <boody> -->

<div id="smooth-wrapper">
	<div id="smooth-content">
		<div id="titleContainerOuter" bind:this={titleContainerOuter}>
			<div id="titleContainerInner" bind:this={titleContainerInner}>
				<MovieMakerTitle>
					my favorite albums!!!!!
				</MovieMakerTitle>
				<div class="text-blue-100 absolute bottom-1 right-1 text-xl">
					⇊
				</div>
			</div>
		</div>

		<div class="h-[100vh] relative">
			<div class="swipe-section h-full flex">
				<div class="w-[30%] m-auto flex flex-col items-center z-1">
					<FacingText3D layers={1} scalar={0.01}>
						<div class="relative overflow-clip">
							<div class="static-noise" bind:this={glitchOverlay}></div>
							<img src={
								(albumData[albumIndex] ? albumData[albumIndex].cover : '')
							} alt="Album art" width="300px" height="300px">
						</div>
					</FacingText3D>
					<span bind:this={albumTitle} class="text-2xl">
						{albumData[0]?.name}
					</span>
					<span bind:this={albumArtist} class="text-xl text-gray-700">
						{albumData[0]?.artist}
					</span>
				</div>
				{#each [...Array(10).keys()] as i (i)}
					<div class="particles absolute w-16"
						style="top:{5 + 90 * Math.random()}%; left: {5 + 90 * Math.random()}%"
					>
						<Text3D gapPx={1}>
							<img src={albumData[albumIndex] ? albumData[albumIndex].particles : ''} alt="">
						</Text3D>
					</div>
				{/each}
			</div>
		</div>
	</div>
</div>

<!-- </boody> -->
<style>
	#titleContainerOuter {
		height:90vh;
		backface-visibility: hidden;
		z-index: 9;
		position: relative;
	}

	#titleContainerInner {
		position: absolute;
		height:100vh;
		width: 100vw;
		top: 0px;
	}

	#smooth-content {
		background-color: var(--color-blue-100);
	}

	.static-noise {
		position: absolute;
		inset: -200%;
		background-image: url("$lib/assets/staticnoise.png");
		z-index: 0;
		animation: shift 0.1s linear infinite both;
	}

	@keyframes shift {
		0% {
			transform: translateX(10%) translateY(10%);
		}

		50% {
			transform: translateX(30%) translateY(-25%);
		}

		100% {
			transform: translateX(-10%) translateY(-10%);
		}
	}
</style>

