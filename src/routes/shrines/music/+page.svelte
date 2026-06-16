<script>
	import { onMount } from "svelte";
	import { gsap } from "gsap/dist/gsap";
	import { ScrollTrigger } from "gsap/dist/ScrollTrigger";
	import { ScrollSmoother } from "gsap/dist/all";
	import ScrambleTextPlugin from "gsap/dist/ScrambleTextPlugin";

	import MovieMakerTitle from "$lib/components/MovieMakerTitle.svelte";
	import PixelBlobs from "./PixelBlobs.svelte";

	let titleContainerOuter, titleContainerInner, albumTitle, albumArtist, albumDesc
	const albumInterval = 25

	let albumData = [{
		name: "I Love My Computer",
		artist: "Ninajirachi",
		cover: "https://upload.wikimedia.org/wikipedia/en/d/dd/I_Love_My_Computer_by_Ninajirachi.png",
		desc: "As a kid I spent a lot of time on the computer, and I was super into EDM which was also at its most popular during my childhood. This album is a loving, more mature evolution of that music I loved. Listening to it evokes the same feelings I had all those years ago. Listening to it always puts me in a better mood, and I really, really hope to hear it at a concert. The visuals are also gorgeous, they make me want to get pictures of cell towers framed on my walls."
	},{
		name: "how i'm feeling now",
		artist: "Charli xcx",
		cover: "https://upload.wikimedia.org/wikipedia/en/b/bd/Charli_XCX_-_How_I%27m_Feeling_Now.png",
		desc: "This was the first album from Charli that I got into, and it remains my favorite to this day. It captures a huge range of emotions and gets them across really effectively, and the industrial noises scratch my brain in just the right way. I would put so much more of her discography here if I weren't trying to restrict myself to one album per artist. Also, I can't put my finger on why, but you can tell it was made during the pandemic."
	},{
		name: "WOMB",
		artist: "Purity Ring",
		cover: "https://upload.wikimedia.org/wikipedia/en/c/c0/Purity_Ring_-_Womb.png",
		desc: "Purity Ring is among the earlier artists I became a big fan of. It was also released during the pandemic, and I leaned on it a lot to get me through hard times. It's like being wrapped in a blanket of sound. Even though I crave much more energetic and noisy music now, I still come back to this album when I'm upset. I also love their other albums, even though my taste has changed so much since discovering them."
	},{
		name: "Bonito Generation",
		artist: "Kero Kero Bonito",
		cover: "https://upload.wikimedia.org/wikipedia/en/2/2c/Kero_Kero_Bonito_-_Bonito_Generation.jpg"
	},{
		name: "SISTER",
		artist: "Frost Children",
		cover: "https://upload.wikimedia.org/wikipedia/en/8/85/Frost_Children_%E2%80%93_Sister.jpg"
	},{
		name: "Frailty",
		artist: "Jane Remover",
		cover: "https://upload.wikimedia.org/wikipedia/en/b/ba/JR_Frailty.png",
		desc: "This album makes me cry. I normally listen to Revengeseekerz and her ♡ EP much more, but this album is a lot more emotionally significant to me. It perfectly captures how it feels to be weird and lonely at a young age, along with a torrent of other feelings, like being upset at people close to you for having cruel beliefs, or feeling irredeemable because your peers are achieving way more than you are. I also listened to this during a breakup, so it's even more emotionally charged for me."
	},{
		name: "WOR$T GIRL IN AMERICA",
		artist: "Slayyyter",
		cover: "https://upload.wikimedia.org/wikipedia/en/7/7a/Worst_Girl_in_America.jpg",
		desc: "I put this on a lot when I'm annoyed, for obvious reasons. The closing track in particular really speaks to me. Even though I'm technically still young I feel like I'm failing to really achieve anything significant or create anything I consider a masterpiece. This was the last album she planned on making because of her music's poor performance in the past (a great injustice IMO), so the lyrics are basically her dying laments. She did her best but couldn't make it big: \"Do you notice all I've done?\""
	}]

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
				scrub: 1
			},
		})
		titleTl.fromTo(titleContainerInner, {rotateY: 0, scale: 1}, {rotateY: '360deg', scale: 0})

		const albumsTl = gsap.timeline()

		const rotateValue = 75
		gsap.set(".albumCover:not(:first-child)", {rotateY: rotateValue})
		gsap.set(".albumCover:not(:first-child)", {filter: "brightness(50%)"})
		gsap.utils.selector("#albumsCarousel")(".albumCover").forEach((e, i) => {
			// item is "focused" at t = i / length-1. duration is arbitrary relative units??
			// move this in
			if (i !== 0){
				albumsTl.fromTo(e, {rotateY: rotateValue}, {rotateY: 0, duration: 1, ease: "power2.inOut"}, i-1)
				albumsTl.fromTo(e, {filter: "brightness(50%)"}, {filter: "brightness(100%)", duration: 1, ease: "power2.inOut"}, i-1)
			}
			// move this out
			if (i !== albumData.length - 1){
				albumsTl.fromTo(e, {rotateY: 0}, {rotateY: -rotateValue, duration: 1, ease: "power2.inOut"}, i)
			}
		})

		albumsTl.fromTo("#albumsCarousel", {xPercent: 0}, {xPercent: -albumInterval * (albumData.length - 1), ease: "none", duration: albumData.length-1}, 0)

		ScrollTrigger.create({
			trigger: ".albums-section",
			start: "top top",
			end: "+=" + (albumData.length - 1) + "00%",
			snap: {
				// ease: "elastic.out",
				snapTo: 1 / (albumData.length - 1),
				delay: 0.1,
				duration: {min: 0.1, max: 0.7},
				onStart: (self) => {
					const index = Math.round(albumsTl.progress() * (albumData.length - 1) + 0.499 * self.direction) // lmao
					gsap.to(albumTitle, {
						scrambleText: {
							text: albumData[index].name,
							chars: 'lowerCase'
						},
						duration: 0.5
					})
					gsap.to(albumArtist, {
						scrambleText: {
							text: albumData[index].artist,
							chars: 'lowerCase'
						},
						duration: 0.5
					})
					gsap.to(albumDesc, {
						scrambleText: {
							text: albumData[index].desc,
							chars: '​'
						},
						duration: 0.5
					})
				}
			},
			scrub: true,
			pin: true,
			animation: albumsTl,
			onUpdate: ()=>{console.log(albumsTl.progress())}
		})
	})
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
			<div class="albums-section h-full flex flex-col justify-center">
				<div id="albumsCarousel" class="w-full h-[300px] overflow-visible">
					<ul class="relative left-[50%] h-full w-full">
						{#each albumData as album, i (i)}
						<li class="absolute object-contain h-full albumCover" style="translate: {i*albumInterval}cqw">
							<img src={
								(album.cover)
							} alt="Album art for {album.name}"
							style="translate: -50%; height: 100%; transform-origin: 0% 40%; perspective: 12cm;">
						</li>
						{/each}
					</ul>
				</div>

				<span bind:this={albumTitle} class="text-2xl text-center text-gray-50">
					{albumData[0]?.name}
				</span>
				<span bind:this={albumArtist} class="text-xl text-gray-400 text-center">
					{albumData[0]?.artist}
				</span>

				<div class="flex flex-col justify-center gap-4 wrap-anywhere text-gray-50">
					<div bind:this={albumDesc}>
						{albumData[0]?.desc}
					</div>
				</div>
			</div>
		</div>
		<br>
		<div style="height: {albumData.length - 1}00vh"></div>
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
		background-color: var(--color-blue-950);
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

