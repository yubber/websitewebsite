<script>
	import { onMount } from "svelte"
	import noise from "$lib/components/PerlinNoise"

	let {pSpacing = 9, tickDelay = 45, pSize = 2, z=0} = $props()
	var canvas, ctx

	onMount(()=>{
		ctx = canvas.getContext("2d")
		canvas.width = window.innerWidth * window.devicePixelRatio
		canvas.height = window.innerHeight * window.devicePixelRatio

		const resizeHandler = () => {
            canvas.width = window.innerWidth * window.devicePixelRatio;
            canvas.height = window.innerHeight * window.devicePixelRatio;
		}

		window.addEventListener('resize', resizeHandler)

		noise.seed(Math.random())

		const interval = setInterval(function() {
			ctx.clearRect(0, 0, window.innerWidth * window.devicePixelRatio, window.innerHeight * window.devicePixelRatio);

			for (let i = 2; i < window.innerWidth * window.devicePixelRatio; i += pSpacing){
				for (let j = 2; j < window.innerHeight * window.devicePixelRatio; j += pSpacing){
					if (Math.random() - Math.abs(noise.perlin3(i/window.innerWidth * window.devicePixelRatio, j/window.innerHeight * window.devicePixelRatio, Date.now() / 1500)) > 0.6) {
						ctx.beginPath()
						ctx.fillStyle = "#0000ff"
						ctx.fillRect(i, j, pSize, pSize)
					}
				}
			}
     	}, tickDelay);

		return () => {
			clearInterval(interval);
			window.removeEventListener('resize', resizeHandler);
		}
	}, )
</script>

<canvas style="--z-prop:{z}"
	bind:this={canvas}
	>
</canvas>

<style>
	canvas {
		display: block;
		position: fixed;
		z-index: var(--z-prop);
	}
</style>