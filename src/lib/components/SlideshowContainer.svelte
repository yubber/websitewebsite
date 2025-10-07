<script>
	import { onMount } from "svelte";

	let {interval=1000, class: className = '', brightness=100,
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
		},{
			url: "url(https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Ftse2.mm.bing.net%2Fth%2Fid%2FOIP.bOI6rgHK3i0bk7BbL0b0GQHaD4%3Fcb%3D12%26pid%3DApi&f=1&ipt=53e57f85b486e30b7afceb0b6b8ae7640626051e21758154c71e1447069b645d)",
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
	<div class="backdrop-filter w-full h-full" style="backdrop-filter: brightness({brightness}%)">
		<slot></slot>
	</div>
</div>