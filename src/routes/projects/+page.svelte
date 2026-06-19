<script>
	import SpinText from "$lib/components/SpinText.svelte";
	import SlideshowContainer from "$lib/components/SlideshowContainer.svelte";
	import "$lib/winxp.css";

	import { gsap } from "gsap/dist/gsap";
	import { ScrollTrigger } from "gsap/dist/ScrollTrigger";
	import { ScrollSmoother } from "gsap/dist/all";
    import { onMount } from "svelte";

	const sidebars = document.getElementsByClassName("sidebar")

	const randIds = [...Array(16).keys()]
		.map(value => ({ value, sort: Math.random() }))
		.sort((a, b) => a.sort - b.sort)
		.map(({ value }) => value)

	onMount(() => {
		gsap.registerPlugin(ScrollTrigger, ScrollSmoother);
		ScrollSmoother.create({
			smooth: 0.3, // how long (in seconds) it takes to "catch up" to the native scroll position
			effects: true, // looks for data-speed and data-lag attributes on elements
			// smoothTouch: 0.1
		});

		let adsTl = gsap.timeline({
			scrollTrigger: {
				trigger: ".smooth-content",
				start: "top top",
				end: "bottom top",
				scrub: 1
			}
		})

		adsTl.to({

		})
	})
</script>

<div id="smooth-wrapper">
	<div id="smooth-content">
		<div class="flex w-72">
			<div class="sidebar">

			</div>
			<div id="games">
				<h1>mauga nipple pve</h1>
				<p>Mauga nipple pve is a popular custom game made using the Overwatch Workshop. Its <a href="https://x.com/MaugaNipplePVE">twitter fan account</a> has over 3k followers.
					The workshop is quite limiting in performance and functionality, so I had to work around that.
				</p>
				<h2>game design</h2>
				<p>In order to exact my revenge on the playerbase, I had to make an extremely addictive game that suited them. From experience as a player and developer, I noticed:</p>
				<ul>
					<li>People are unwilling to learn games that don't involve the standard FPS gameplay</li>
					<li>They stay much longer on easy games, and almost immediately leave when they see the defeat screen</li>
					<li>They don't mind playing mind-numbingly easy games, even when it's just shooting enemies with no lose condition</li>
					<li>They don't read</li>
				</ul>
				<h2>problem solving</h2>
				<h3>enemy quantity</h3>
				<p>I wanted the game to have a large number of enemies in order to achieve the kind of brainrot gameplay I envisioned. To mitigate the performance impact of having many bots with their own logic, I used a map with simple geometry so that the pathfinding could be extremely low cost. I also</p>
			</div>
		</div>
	</div>
</div>

<style>
	@import "tailwindcss";
	.sidebar {
		@media only screen and (min-width: 1100px) {
			display: none;
		}
		@apply w-72;
		overflow: hidden;
	}

	.retrobtn {
		box-sizing: content-box;
		border: solid 3px transparent;
		height: 2.5em;
		padding: 0 1.75em;
		border-radius: 1em;
		box-shadow: inset 0 0 0 3px rgba(255, 255, 255, 0.2), inset 0 -1.25em 1.25em -1.25em #494b4f;
		--ini: circle farthest-side at;
		--lst: 0, transparent 100%, #383d41;
		--set: bottom 1.25em/ 0.625em 0.625em no-repeat padding-box;
		background: radial-gradient(var(--ini) 100% var(--lst)) left 0 var(--set), radial-gradient(var(--ini) 0 var(--lst)) right 0 var(--set), linear-gradient(#64686a, #45494d 50%, #383d41 0) padding-box, linear-gradient(#2e3034, #1e2024) border-box;
		/* color: #e9eae9; */
		font: inherit;
		color: whitesmoke;
		text-shadow: 1px 1px #434343, 1px 1px 3px #323232;
		&:active {
			filter: brightness(0.5);
			box-shadow: inset 0 0 0 3px rgba(255, 255, 255, 0.849), inset 0 -1.25em 1.25em -1.25em #494b4f;
			/* border-top: 1px; */
			/* background: radial-gradient(var(--lst) 100% var(--ini)) left 0 var(--set), radial-gradient(var(--lst) 0 var(--ini)) right 0 var(--set), linear-gradient(#64686a, #45494d 50%, #383d41 0) padding-box, linear-gradient(#2e3034, #1e2024) border-box; */
		}
	}

	.dlbtn {
		width: 100%;
		height: 100%;
		background: linear-gradient(
			var(--color-green-700) 0%,
			var(--color-green-200) 100%
		)
	}

	.metal {
		background: linear-gradient(
			135deg,
			#999 5%,
			#fff 10%,
			#ccc 30%,
			#ddd 50%,
			#ccc 70%,
			#fff 80%,
			#999 95%
		);
	}
</style>