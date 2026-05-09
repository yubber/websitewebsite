<script>
    import { onMount } from "svelte";
	import MovieMakerTitle from "$lib/components/MovieMakerTitle.svelte";

	import { gsap } from "gsap";
	import { ScrollTrigger } from "gsap/ScrollTrigger";
	let titleContainer

	onMount(()=>{
		gsap.registerPlugin(ScrollTrigger);

		// setInterval()
		let titleTl = gsap.timeline({
			scrollTrigger: {
				trigger: titleContainer,
				start: "top top",
				end: "bottom top",
				markers: true
			}
		})
		titleTl.to(titleContainer, {x:500, rotateY: 720, scale: 50})
	})



	// let scrollTl = gsap.timeline({
	// 	scrollTrigger: {
	// 		trigger:
	// 	}
	// })
</script>

<div bind:this={titleContainer}>
	<MovieMakerTitle>
		my favorite albums!!!!!
	</MovieMakerTitle>
</div>

<div class="h-[100vh]">
	uwa
</div>

<style>
</style>

