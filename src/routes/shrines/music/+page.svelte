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
		artist: "Kero Kero Bonito"
	},{
		name: "SISTER",
		artist: "Frost Children"
	},{
		name: "Frailty",
		artist: "Jane Remover",
		desc: "This album makes me cry. I normally listen to Revengeseekerz and her ♡ EP much more, but this album is a lot more emotionally significant to me. It perfectly captures how it feels to be weird and lonely at a young age, along with a torrent of other feelings, like being upset at people close to you for having cruel beliefs, or feeling irredeemable because your peers are achieving way more than you are. I also listened to this during a breakup, so it's even more emotionally charged for me."
	},{
		name: "WOR$T GIRL IN AMERICA",
		artist: "Slayyyter",
		desc: "I put this on a lot when I'm annoyed, for obvious reasons. The closing track in particular really speaks to me. Even though I'm technically still young I feel like I'm failing to really achieve anything significant or create anything I consider a masterpiece. This was the last album she planned on making because of her music's poor performance in the past (a great injustice IMO), so the lyrics are basically her dying laments. She did her best but couldn't make it big: \"Do you notice all I've done?\""
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
			<div class="swipe-section h-full flex flex-row items-center justify-items-start lg:w-[70vw] mx-auto">
				<div class="flex flex-col items-center z-9 flex-1">
					<FacingText3D layers={1} scalar={0.01}>
						<div class="relative overflow-clip">
							<div class="static-noise" bind:this={glitchOverlay}></div>
							<img src={
								(albumData[albumIndex] ? albumData[albumIndex].cover : '')
							} alt="Album art" width="300px" height="300px">
						</div>
					</FacingText3D>
					<span bind:this={albumTitle} class="text-2xl text-center text-gray-50">
						{albumData[0]?.name}
					</span>
					<span bind:this={albumArtist} class="text-xl text-gray-400 text-center">
						{albumData[0]?.artist}
					</span>
				</div>

				<div class="flex flex-col justify-center gap-4 wrap-anywhere flex-2 text-gray-50">
					<div bind:this={albumDesc}>
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
		background-color: var(--color-blue-950);
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

