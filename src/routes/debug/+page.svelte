<script>
	import { onMount } from "svelte";
	import { gsap } from "gsap/dist/gsap";
	import { ScrollSmoother } from "gsap/dist/all";

	import { ScrollTrigger } from "gsap/dist/ScrollTrigger";

	onMount(()=>{
		gsap.registerPlugin(ScrollTrigger, ScrollSmoother)

		ScrollSmoother.create({
			smooth: 0.3, // how long (in seconds) it takes to "catch up" to the native scroll position
			effects: true, // looks for data-speed and data-lag attributes on elements
			// smoothTouch: 0.1
		});

		gsap.set(".slide:not(:first-child)", { xPercent: 100 });
		gsap.set(".slide .heading", { opacity: 0 });

		const tl = gsap.timeline();
		tl.to(".slide:not(:first-child)", {
			ease: "none",
			xPercent: 0,
			stagger: 1,
			duration: 1
		}).to(
		".slide .heading",
		{
			opacity: 1,
			duration: 1,
			stagger: 1
		},
		"<"
		);

		ScrollTrigger.create({
			trigger: ".slides",
			start: "top top",
			end: "+=500%",
			scrub: true,
			pin: true,
			animation: tl
			//markers: true
		});
	})

</script>


<div id="smooth-wrapper">
	<div id="smooth-content">
<section class="section">
	<div>
		<h1>Reveal Sections on Scroll</h1>
		<p>GSAP & ScrollTrigger - <span>right-to-left horizontal animation</span></p>
		<p>👇 Scroll down</p>
	</div>
</section>
<section class="section-slides">
	<div class="slides">
		<div class="slide">
			<figure>
				<img width="1920" height="1280" src="https://assets.codepen.io/162656/gallery-edinburgh.jpg" alt="edinburgh" />
				<figcaption>
					<h2 class="heading">Edinburgh</h2>
				</figcaption>
			</figure>
		</div>
		<div class="slide">
			<figure>
				<img width="1920" height="1005" src="https://assets.codepen.io/162656/gallery-berlin.jpg" alt="berlin" />
				<figcaption>
					<h2 class="heading">Berlin</h2>
				</figcaption>
			</figure>
		</div>
		<div class="slide">
			<figure>
				<img width="1920" height="1282" src="https://assets.codepen.io/162656/gallery-havana.jpg" alt="havana" />
				<figcaption>
					<h2 class="heading">Havana</h2>
				</figcaption>
			</figure>
		</div>
		<div class="slide">
			<figure>
				<img width="1920" height="1279" src="https://assets.codepen.io/162656/gallery-london.jpg" alt="london" />
				<figcaption>
					<h2 class="heading">London</h2>
				</figcaption>
			</figure>
		</div>
		<div class="slide">
			<figure>
				<img width="1920" height="1439" src="https://assets.codepen.io/162656/gallery-athens.jpg" alt="athens" />
				<figcaption>
					<h2 class="heading">Athens</h2>
				</figcaption>
			</figure>
		</div>
		<div class="slide">
			<figure>
				<img width="1920" height="1281" src="https://assets.codepen.io/162656/gallery-vienna.jpg" alt="vienna" />
				<figcaption>
					<h2 class="heading">Vienna</h2>
				</figcaption>
			</figure>
		</div>
	</div>
</section>
<section class="section">
	<h2>Thank you!</h2>
</section>
</div>
</div>

<style>
	/* BASIC STYLES
	–––––––––––––––––––––––––––––––––––––––––––––––––– */
	@import url("https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100..900;1,100..900&display=swap");

	* {
		box-sizing: border-box;
	}

	body {
		font-family: "Montserrat", sans-serif;
		margin: 0;
	}

	.section {
		display: flex;
		align-items: center;
		justify-content: center;
		padding: 15px;
		height: 100vh;
		text-align: center;
		color: white;
		background: #003049;
	}

	.section span {
		text-decoration: underline;
	}

	.section-slides {
		margin-top: -1px;
	}

	/* MAIN STYLES
	–––––––––––––––––––––––––––––––––––––––––––––––––– */
	.slides {
		display: grid;
		overflow: hidden;
	}

	.slide {
		grid-area: 1/1;
	}

	.slide figure {
		margin: 0;
		position: relative;
		height: 100vh;
	}

	.slide img {
		width: 100%;
		height: 100%;
		object-fit: cover;
		background: #f1faee;
	}

	.slide figcaption {
		display: flex;
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		align-items: center;
		background: rgba(0, 0, 0, 0.15);
	}

	.slide .heading {
		display: inline-block;
		padding: 5px 15px;
		text-align: center;
		font-size: clamp(2.5rem, 2vh, 5rem);
		line-height: 1;
		font-weight: bold;
		color: #d62828;
		background: #fcbf49;
		transform: rotate(-90deg) translateX(-50%);
		transform-origin: left top;
	}
</style>