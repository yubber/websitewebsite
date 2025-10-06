<script>
	import { onMount } from "svelte";

	let {interval=1000, class: className = '',
		slides=[{
			url: "url(https://frutigeraeroarchive.org/images/wallpapers/materialdictionary206/materialdictionary206_15.jpg)",
			styles: "bg-cover bg-no-repeat"
		},{
			url: "url(https://frutigeraeroarchive.org/images/wallpapers/anime/anime_15.jpg)",
			styles: "bg-cover bg-no-repeat bg-center"
		},{
			url: "url(https://y2kid.xyz/backgrounds/Rainbow.bmp)",
			styles: "bg-repeat"
		},{
			url: "url(https://frutigeraeroarchive.org/images/wallpapers/windows_xp/windows_xp_16.jpg)",
			styles: "bg-cover bg-no-repeat"
		},{
			url: "url(https://frutigeraeroarchive.org/images/wallpapers/windows_xp/windows_xp_143.jpg)",
			styles: "bg-cover bg-no-repeat"
		},{
			url: "url(https://thegardenofmadeline.neocities.org/pinkmovingstar_bg_tile.gif)",
			styles: "bg-repeat"
		},{
			url: "url(https://frutigeraeroarchive.org/images/wallpapers/vectordelia/vectordelia_29.jpg)",
			styles: "bg-cover bg-no-repeat bg-center"
		},{
			url: "url(https://thegardenofmadeline.neocities.org/gifs/wiirotation_gif.gif)",
			styles: "bg-contain bg-no-repeat bg-center"
		}], extraSlides=[],
		children, ...rest } = $props()

	slides = slides.concat(extraSlides)

	let i = $state(0);

	onMount(()=>{
		setInterval(()=>{
			i = (i + 1) % slides.length
		}, window.matchMedia('(prefers-reduced-motion: reduce)').matches ? 10000 : interval)
	})
</script>

<div class="{slides[i].styles} {className}"
	style="background-image: {slides[i].url}">
	<div class="backdrop-filter backdrop-brightness-60 w-full h-full">
		<slot></slot>
	</div>
</div>