<script>
    import { onMount } from "svelte";
	import MovieMakerTitle from "$lib/components/MovieMakerTitle.svelte";

	import { gsap } from "gsap";
	import { ScrollTrigger } from "gsap/ScrollTrigger";
	import { ScrollSmoother } from "gsap/all";
	let titleContainerOuter, titleContainerInner

	onMount(()=>{
		gsap.registerPlugin(ScrollTrigger, ScrollSmoother);

		// create the scrollSmoother before your scrollTriggers
		ScrollSmoother.create({
			smooth: 0.3, // how long (in seconds) it takes to "catch up" to the native scroll position
			effects: true, // looks for data-speed and data-lag attributes on elements
			// smoothTouch: 0.1
		});

		// setInterval()
		let titleTl = gsap.timeline({
			scrollTrigger: {
				trigger: titleContainerOuter,
				start: "top top",
				end: "bottom top",
				scrub: 1,
			}
		})
		titleTl.to(titleContainerInner, {rotateY: 360, scale: 0.5})
	})

	// let scrollTl = gsap.timeline({
	// 	scrollTrigger: {
	// 		trigger:
	// 	}
	// })
</script>
<!-- <boody> -->

<div id="titleContainerOuter" bind:this={titleContainerOuter}>
	<div bind:this={titleContainerInner} class="h-full w-full">
		<MovieMakerTitle>
			my favorite albums!!!!!
		</MovieMakerTitle>
	</div>
	<div class="text-blue-100 absolute bottom-0">
		⇊
	</div>
</div>

<div class="h-[100vh]">
	I Love My Computer
	
</div>

<!-- </boody> -->
<style>
	#titleContainerOuter {
		height:100vh;
		width: 100vw;
		backface-visibility: hidden;
	}

	boody {
		background-color: var(--color-blue-50);
		width: 100vw;
	}
</style>

