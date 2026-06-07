<script>
	import { onMount } from "svelte"
	let {pSpacing = 9, tickDelay = 60, pSize = 2.4, xOffset = 0, yOffset = 0, z=0, color="#0000ff"} = $props()
	var canvas, ctx, hidden, hidectx, lastFrameTime
	var particles = {} // easier mgmt than array?
	var particleIndex = 0

	/* todo
	- optimize duplicate particle positions
	*/

	onMount(()=>{
		ctx = canvas.getContext("2d")
		canvas.width = window.innerWidth * window.devicePixelRatio
		canvas.height = window.innerHeight * window.devicePixelRatio
		window.addEventListener('resize', () => {
            canvas.width = window.innerWidth * window.devicePixelRatio;
            canvas.height = window.innerHeight * window.devicePixelRatio;
		})

		hidectx = hidden.getContext("2d")
		hidden.width = pSize
		hidden.height = pSize
		hidectx.beginPath()
		hidectx.fillStyle = color
		hidectx.fillRect(0, 0, pSize, pSize)

		function animation(time) {
			if (time - lastFrameTime >= tickDelay){
				lastFrameTime = time
				ctx.clearRect(0, 0, window.innerWidth * window.devicePixelRatio, window.innerHeight * window.devicePixelRatio);

				for (let i in particles) {
					particles[i].tick();
				}
     		}
			requestAnimationFrame(animation)
		}

		lastFrameTime = window.performance.now()
		requestAnimationFrame(animation)
	})

	class Particle {
		constructor(x, y, context){
			this.lifeLeft = 0 + 240 * Math.random() * (Math.random() > 0.9 ? 2.5 : 1)
			this.x = x
			this.y = y
			this.ctx = context
			this.i = particleIndex
			particleIndex++
			particles[this.i] = this
			this.tick()
		}

		tick(){
			this.lifeLeft-= tickDelay
			if (this.lifeLeft >= 0){
				ctx.drawImage(hidden, this.x, this.y);
				if (this.lifeLeft < 500) {
					this.x += pSpacing * Math.round((Math.random() - 0.5) * 8)
					this.y += pSpacing * Math.round((Math.random() - 0.5) * 8)
				}
			} else {
				delete particles[this.i]
			}
		}
	}

	let offsetCache = []
	for (let x = -pSpacing*5; x <=pSpacing*5; x += pSpacing){
		for (let y = -pSpacing*5; y <=pSpacing*5; y += pSpacing){
			if (x**2 + y**2 <= (pSpacing*6)**2) {
				offsetCache.push([x,y])
			}
		}
	}

	let genParticles = () => {
		for (const [x, y] of offsetCache) {
			new Particle(x + Math.floor((event.clientX + xOffset) / pSpacing) * pSpacing + 2, y + Math.floor((event.clientY + yOffset) / pSpacing) * pSpacing, ctx)
		}
	}

</script>

<svelte:window onmousemove={genParticles}></svelte:window>

<canvas id="mousePoo" style="--z-prop:{z}"
	bind:this={canvas}
	>
</canvas>

<canvas style="display: none;" bind:this={hidden}>
</canvas>

<style>
	canvas {
		width: 100vw;
		height: 100vh;
		position: absolute;
		z-index: var(--z-prop);
	}
</style>