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
	import PixelBlobs from "./PixelBlobs.svelte";

	let titleContainerOuter, titleContainerInner, albumTitle, glitchOverlay, albumArtist, albumDesc
	let albumIndex = $state(0);
	let animating = $state();

	onMount(()=>{
		gsap.registerPlugin(ScrollTrigger, ScrollSmoother, ScrambleTextPlugin);

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
				// pin: "#pixBlobsContainer",
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

			gsap.to(glitchOverlay, {
				opacity: "100%",
				duration: 0.375,
				onComplete: ()=>{albumIndex = index}
			})
			gsap.fromTo(glitchOverlay,{
				opacity: "100%"
			},{
				opacity: "0%",
				duration: 0.37,
				delay: 0.38,
				onComplete: () => {
					animating = false
				}
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
		desc: "I grew up spending most of my childhood on the computer. EDM was also in its heyday at the time, and it was all I listened to as a child. This album is a really authentic and personal reflection of those experiences."
	},{
		name: "how i'm feeling now",
		artist: "Charli xcx",
		cover: "https://upload.wikimedia.org/wikipedia/en/b/bd/Charli_XCX_-_How_I%27m_Feeling_Now.png",
		desc: "This was the first album from Charli that I got into. I think her best work is either this or Pop 2."
	},{
		name: "WOMB",
		artist: "Purity Ring",
		cover: "https://upload.wikimedia.org/wikipedia/en/c/c0/Purity_Ring_-_Womb.png",
		desc: ""
	}]
</script>
<!-- <boody> -->

<PixelBlobs></PixelBlobs>

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
			<div class="swipe-section h-full flex justify-center items-center px-4 lg:">
				<div class="w-[30%] flex flex-col items-center z-9">
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

				<div class="flex flex-col justify-center gap-4">
					<div class="text-center" bind:this={albumDesc}>
						{albumData[0]?.desc}
					</div>
				</div>
			</div>
		</div>
	</div>
</div>

<!-- </boody> -->
<style>
	#titleContainerOuter {
		height:90vh;
		backface-visibility: hidden;
		position: relative;
		z-index: 9;
	}

	#titleContainerInner {
		position: absolute;
		z-index: 9;
		height:100vh;
		width: 100vw;
		top: 0px;
	}

	:global(body) {
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

