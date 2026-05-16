<script>
	import widgetblack from "$lib/assets/face+black+transparent.png"

	import { onMount } from "svelte";
	import { gsap } from "gsap";
	import { ScrollTrigger } from "gsap/ScrollTrigger";
	import { ScrollSmoother } from "gsap/all";

	import MovieMakerTitle from "$lib/components/MovieMakerTitle.svelte";
	import SpinText from "$lib/components/SpinText.svelte";

	let titleContainerOuter, titleContainerInner, glitchOverlay, particles
	let albumIndex = -1;
	let animating;

	import widget from "$lib/assets/face+black+transparent.png";

	onMount(()=>{
		gsap.registerPlugin(ScrollTrigger, ScrollSmoother);

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
			}
		})
		titleTl.to(titleContainerInner, {rotateY: 360, scale: 0.5})

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
				isScrollingDown && intentObserver.disable();
				return;
			}

			gsap.to(glitchOverlay, {
				visibility: "visible",
				duration: 0.75,
				onComplete: () => {
					animating = false;
				}
			});

			gsap.to(particles, {
				rotateY: 90,
				duration: 0.375,
				onComplete: () => {
					albumIndex = index

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
				intentObserver.enable();
				albumIndex = 0
				changeAlbum(albumIndex + 1, true);
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
		cover: "",
		particles: widget,
	},{
		name: "how i'm feeling now",
		artist: "Charli xcx",
		cover: "",
		particles: ""
	}]
</script>
<!-- <boody> -->

<div id="smooth-wrapper">
	<div id="smooth-content">
		<div id="titleContainerOuter" bind:this={titleContainerOuter}>
			<div id="titleContainerInner" bind:this={titleContainerInner} class="h-full w-full">
				<MovieMakerTitle>
					my favorite albums!!!!!
				</MovieMakerTitle>
			</div>
			<div class="text-blue-100 absolute bottom-1 right-1 text-xl">
				⇊
			</div>
		</div>

		<div class="h-[100vh] absolute top-0 swipe-section">
			<SpinText>
				{albumData[albumIndex].name}
			</SpinText>
			{#each [...Array(10).keys()] as i (i)}
				<div class="particles">

				</div>
			{/each}
		</div>
	</div>
</div>

<!-- </boody> -->
<style>
	#titleContainerOuter {
		height:100vh;
		backface-visibility: hidden;
	}

	#titleContainerInner {
		position: absolute;
	}

	#smooth-content {
		background-color: var(--color-blue-50);
	}
</style>

