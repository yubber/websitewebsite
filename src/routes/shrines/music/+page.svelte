<script>
	import widgetblack from "$lib/assets/face+black+transparent.png"

	import { onMount } from "svelte";
	import { gsap } from "gsap";
	import { ScrollTrigger } from "gsap/ScrollTrigger";
	import { ScrollSmoother } from "gsap/all";
	import ScrambleTextPlugin from "gsap/ScrambleTextPlugin";

	import MovieMakerTitle from "$lib/components/MovieMakerTitle.svelte";
	import StaticNoise from "$lib/components/StaticNoise.svelte";
	import SpinText from "$lib/components/SpinText.svelte";

	let titleContainerOuter, titleContainerInner, albumTitle, particles
	let albumIndex = 0;
	let animating;

	import widget from "$lib/assets/face+black+transparent.png";

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
				{rotateY: 0},
				{rotateY: 90,
				duration: 0.375,
				onComplete: () => {
					albumIndex = index
					gsap.to(particles, {
						rotateY: 180,
						duration: 0.375,
						onComplete: () => {
							animating = false
						}
					})
				}
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
	},{
		name: "how i'm feeling now",
		artist: "Charli xcx",
		cover: "https://upload.wikimedia.org/wikipedia/en/b/bd/Charli_XCX_-_How_I%27m_Feeling_Now.png",
		particles: ""
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

		<div class="h-[100vh] bg-blue-100 relative">
			<div class="swipe-section h-full flex">
				<div class="w-[30%] m-auto flex flex-col items-center">
					<StaticNoise class="w-full h-full absolute z-0"></StaticNoise>
					<img src={
						animating ? 'https://media1.tenor.com/m/88dnH_mHRLAAAAAC/static-tv-static.gif' :
						(albumData[albumIndex] ? albumData[albumIndex].cover : '')
					} alt="Album art" width="100%">
					<span bind:this={albumTitle}>
						{albumData[albumIndex][0]?.name}
					</span>
				</div>
				{#each [...Array(10).keys()] as i (i)}
					<div class="particles absolute w-2">
						<img src={albumData[albumIndex] ? albumData[albumIndex].particles : ''} alt="">
					</div>
				{/each}
			</div>
		</div>
	</div>
</div>

<!-- </boody> -->
<style>
	#titleContainerOuter {
		height:30vh;
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
		background-color: var(--color-blue-50);
	}
</style>

