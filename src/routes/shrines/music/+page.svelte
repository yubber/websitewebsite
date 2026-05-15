<script>
	import widgetblack from "$lib/assets/face+black+transparent.png"

    import { onMount } from "svelte";
	import { gsap } from "gsap";
	import { ScrollTrigger } from "gsap/ScrollTrigger";
	import { ScrollSmoother } from "gsap/all";

	import MovieMakerTitle from "$lib/components/MovieMakerTitle.svelte";
	import SpinText from "$lib/components/SpinText.svelte";
	let titleContainerOuter, titleContainerInner

	import widget from "$lib/assets/face+black+transparent.png"
	import pop2 from "$lib/assets/pop2.png"

	onMount(()=>{
		gsap.registerPlugin(ScrollTrigger, ScrollSmoother);

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

	let albumData = [{
		name: "",
		cover: "",
		particles: "",
		bgThing: ""
		}
	]
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

	<div class="h-[100vh] absolute top-0">
		I Love My Computer
		<SpinText>
			<img src={widgetblack} alt="">
		</SpinText>
		{#each [...Array(5).keys()] as i}
			<div>

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

