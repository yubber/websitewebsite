<script>
	import { onMount } from "svelte"
	var canvas, ctx
	var particles = {} // easier mgmt than array?
	var particleIndex = 0

	/* todo
	- detect duplicate particle positions
	*/

	onMount(()=>{
		ctx = canvas.getContext("2d")
		canvas.width = window.innerWidth * window.devicePixelRatio
		canvas.height = window.innerHeight * window.devicePixelRatio
		window.addEventListener('resize', () => {
            canvas.width = window.innerWidth * window.devicePixelRatio;
            canvas.height = window.innerHeight * window.devicePixelRatio;
		})

		setInterval(function() {
			ctx.clearRect(0, 0, window.innerWidth * window.devicePixelRatio, window.innerHeight * window.devicePixelRatio);

			for (let i in particles) {
				particles[i].tick();
			}
     	}, 30);
	})

	class Particle {
		constructor(x, y, context){
			this.lifeLeft = 0 + 390 * Math.random()
			this.x = x
			this.y = y
			this.ctx = context
			this.i = particleIndex
			particleIndex++
			particles[this.i] = this
			this.tick()
		}

		tick(){
			this.lifeLeft-= 30
			if (this.lifeLeft >= 0){
				this.ctx.beginPath()
				this.ctx.fillStyle = "#0000ed"
				this.ctx.fillRect(this.x, this.y, 2,2)
			} else {
				delete particles[this.i]
			}
		}
	}

	let offsetCache = []
	for (let x = -40; x <=40; x += 8){
		for (let y = -40; y <=40; y += 8){
			if (x**2 + y**2 <= 32**2) {
				offsetCache.push([x,y])
			}
		}
	}

	let genParticles = () => {
		for (const [x, y] of offsetCache) {
			new Particle(x + Math.floor(event.clientX / 8) * 8, y + Math.floor(event.clientY / 8) * 8, ctx)
		}
	}

</script>

<svelte:window onmousemove={genParticles}></svelte:window>

<canvas id="mousePoo"
	bind:this={canvas}
	>
</canvas>

<style>
	canvas {
		width: 100vw;
		height: 100vh;
		position: absolute;
	}
</style>