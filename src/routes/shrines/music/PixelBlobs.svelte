<script>
	import { onMount } from "svelte"
	import { createNoise3D } from "simplex-noise"

	let {pSpacing = 9, tickDelay = 60, pSize = 2.5, z=0, canvas = $bindable()} = $props()
	var ctx, hidden, hidectx, lastFrameTime

	onMount(()=>{
		ctx = canvas.getContext("2d")
		canvas.width = window.innerWidth * window.devicePixelRatio
		canvas.height = window.innerHeight * window.devicePixelRatio

		hidectx = hidden.getContext("2d")
		hidden.width = pSize
		hidden.height = pSize

		const resizeHandler = () => {
            canvas.width = window.innerWidth * window.devicePixelRatio;
            canvas.height = window.innerHeight * window.devicePixelRatio;
		}

		window.addEventListener('resize', resizeHandler)

		// draw on hidden canvas to cache image
		hidectx.beginPath()
		hidectx.fillStyle = "#6969ff"
		hidectx.fillRect(0, 0, pSize, pSize)

		const noise3D = createNoise3D();

		const churnSlow = window.matchMedia(`(prefers-reduced-motion: reduce)`).matches ? 4096 : 1024
		function animation(time) {
			if (time - lastFrameTime >= tickDelay){
				lastFrameTime = time
				ctx.clearRect(0, 0, window.innerWidth * window.devicePixelRatio, window.innerHeight * window.devicePixelRatio);

				for (let i = 2; i < window.innerWidth * window.devicePixelRatio; i += pSpacing){
					for (let j = 2; j < window.innerHeight * window.devicePixelRatio; j += pSpacing){
						if (Math.random() - Math.abs(noise3D(i/512, j/512, time/churnSlow)) > 0.5) {
							ctx.drawImage(hidden, i, j);
						}
					}
				}
			}

			requestAnimationFrame(animation)
     	};
		lastFrameTime = window.performance.now()
		requestAnimationFrame(animation)
		console.log(lastFrameTime)

		return () => {
			window.removeEventListener('resize', resizeHandler);
		}
	}, )
</script>

<canvas style="--z-prop:{z}" id="mainCanvas"
	bind:this={canvas}
	>
</canvas>

<canvas style="display: none;" bind:this={hidden}>
</canvas>

<style>
	#mainCanvas {
		display: block;
		position: fixed;
		z-index: var(--z-prop);
	}
</style>