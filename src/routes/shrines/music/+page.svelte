<script>
	import { onMount } from "svelte";
	import { gsap } from "gsap/dist/gsap";
	import { ScrollTrigger } from "gsap/dist/ScrollTrigger";
	import { ScrollSmoother } from "gsap/dist/all";
	import ScrambleTextPlugin from "gsap/dist/ScrambleTextPlugin";

	import MovieMakerTitle from "$lib/components/MovieMakerTitle.svelte";
	import PixelBlobs from "./PixelBlobs.svelte";
	import SpinText from "$lib/components/SpinText.svelte";
    import { invalidate } from "$app/navigation";

	let titleContainerOuter, titleContainerInner, albumTitle, albumArtist, albumDesc
	const albumInterval = 25

	let albumData = [{
		name: "I Love My Computer",
		artist: "Ninajirachi",
		cover: "https://upload.wikimedia.org/wikipedia/en/d/dd/I_Love_My_Computer_by_Ninajirachi.png",
		desc: "As a kid I spent a lot of time on the computer, and I was super into EDM which was also at its most popular during my childhood. This album is a loving, more mature evolution of that music I loved. Listening to it evokes the same feelings I had all those years ago. It always puts me in a better mood, and I really, really hope to hear it at a concert. The visuals are also gorgeous, they make me want to get pictures of cell towers framed on my walls. I also really appreciate her cheeky use of Times New Roman here. I think it's the next Comic Sans. I say \"next\" because Comic Sans is used so prolifically it's lost its edge as an intentionally horrible-looking font, and it's pretty much become entirely appropriate, even tasteful, to use it wholeheartedly for cheeky, low-effort situations. Of course, Times is nowhere as hideous as Comic Sans. I'm personally more repulsed by Calibri but there seem to be many who're simply ambivalent towards it, and it doesn't have the litany of \"objective\" criticisms that Comic Sans does. Times doesn't have nearly that many either, but there's still a familiar stench of tastelessness. It has a huge target painted on its back for being the default font in many cases, like the unstyled text in a beginner's first 'Hello World!' HTML page, or being the first font in reach of anyone making a pitiable grasp at formality and gravitas (which, fittingly enough, includes the Trump administration). That popularity is a major factor in making a typeface shift from disliked to reviled, just like it was for Comic Sans. It's also developing a history of misuse: while it has great readability in print, its legibility greatly suffers on screens and it can even be challenging to read in smaller sizes. In an age where most documents are almost exclusively read in digital form and printers sit collecting dust, Times' poor screen readability has been making it a questionable choice for a long time. Artists who are far more in tune with the culture seem to agree: Ninajirachi and Playboi Carti feature tastefully distorted Times New Roman in their music videos and album covers respectively, and Charli XCX is using it for her singles art as she continues her streak of intentionally ugly covers."
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
		cover: "https://upload.wikimedia.org/wikipedia/en/2/2c/Kero_Kero_Bonito_-_Bonito_Generation.jpg",
		desc: ""
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
		desc: "I put this on a lot when I'm annoyed, for obvious reasons. The closing track in particular really speaks to me. Even though I'm technically still young I feel like I'm failing to really achieve anything significant or create anything I consider a masterpiece. This was the last album she planned on making because of her music's poor performance in the past (a great injustice in my opinion, she had her finger on the pulse since her debut EP), so the lyrics are basically her dying laments. She did her best but couldn't make it big: \"Do you notice all I've done?\""
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

		const rotateValue = 45
		gsap.set(".albumCover:not(:first-child)", {rotateY: -rotateValue})
		gsap.set(".albumCover:not(:first-child)", {filter: "brightness(50%)"})
		gsap.utils.selector("#albumsCarousel")(".albumCover").forEach((e, i) => {
			// item is "focused" at t = i / length-1. duration is arbitrary relative units??
			if (i !== 0){
				// move this in
				albumsTl.fromTo(e, {rotateY: -rotateValue}, {rotateY: 0, duration: 1, ease: "power2.inOut"}, i-1)
				albumsTl.fromTo(e, {filter: "brightness(50%)"}, {filter: "brightness(100%)", duration: 1, ease: "power2.inOut"}, i-1)

				// text transition
				albumsTl.to(albumTitle, {
					scrambleText: {
						text: albumData[i].name,
						chars: 'lowerCase'
					},
					duration: 0.7
				}, i-0.7)
				albumsTl.to(albumArtist, {
					scrambleText: {
						text: albumData[i].artist,
						chars: 'lowerCase'
					},
					duration: 0.7
				}, i-0.7)
				albumsTl.to(albumDesc, {
					scrambleText: {
						text: albumData[i].desc,
						chars: '​'
					},
					duration: 0.7
				}, i-0.7)
			}
			// move this out
			if (i !== albumData.length - 1){
				albumsTl.fromTo(e, {filter: "brightness(100%)"}, {filter: "brightness(50%)", duration: 1, ease: "power2.inOut"}, i)
				albumsTl.fromTo(e, {rotateY: 0}, {rotateY: rotateValue, duration: 1, ease: "power2.inOut"}, i)
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
				delay: 0,
				duration: {min: 0.1, max: 0.5}
			},
			scrub: true,
			pin: true,
			invalidateOnRefresh: true,
			animation: albumsTl
		})
	})
</script>
<!-- <boody> -->

<PixelBlobs></PixelBlobs>

<div class="fixed flex items-center justify-center h-[100vh] w-[100vw] opacity-25">
	<SpinText gapPx={4}>
		<img src="https://freight.cargo.site/t/original/i/facff737252a9f4a9021e756b104b84cd54a76d59381b956e493c6c48d2dd7aa/u-favicon.png" alt="">
	</SpinText>
</div>

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

		<div class="h-[100vh]">
			<div class="albums-section perspective-origin-center perspective-midrange transform-3d">
				<div class="relative top-[40%] transform-3d flex flex-col justify-start">
					<div id="albumsCarousel" class="w-full h-[300px] overflow-visible transform-3d">
						<ul class="relative left-[50%] h-full w-full transform-3d">
							{#each albumData as album, i (i)}
							<li class="absolute object-contain h-full albumCover transform-3d" style="translate: {i*albumInterval}cqw; transform-origin: 0% 40%;">
								<img src={
									(album.cover)
								} alt="Album art for {album.name}"
								style="height: 100%; translate: -50%;">
							</li>
							{/each}
						</ul>
					</div>


					<span bind:this={albumTitle} class="text-4xl text-center text-gray-50 squishroman pt-4">
						{albumData[0]?.name}
					</span>
					<span bind:this={albumArtist} class="text-xl text-gray-400 text-center font-mono">
						{albumData[0]?.artist}
					</span>

					<div class="flex flex-col justify-center gap-4 wrap-anywhere text-gray-50 lg:px-12 py-4 arialNarrow">
						<div bind:this={albumDesc}>
							{albumData[0]?.desc}
						</div>
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

