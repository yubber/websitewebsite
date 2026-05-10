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

			// for (let i = 0; i < 20; i++){
			// 	new Particle(Math.floor(window.innerWidth * window.devicePixelRatio * Math.random() / 8) * 8 + 2,
			// 		Math.floor(window.innerHeight * window.devicePixelRatio * Math.random() / 8) * 8, ctx)
			// }
     	}, 80);
	})

	let [pSpacing, pSize] = [9, 2.5]

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
			this.lifeLeft-= 80
			if (this.lifeLeft >= 0){
				this.ctx.beginPath()
				this.ctx.fillStyle = "#0000ff"
				this.ctx.fillRect(this.x, this.y, pSize,pSize)
				if (this.lifeLeft < 500) {
					this.x += pSpacing * Math.round((Math.random() - 0.5) * 5)
					this.y += pSpacing * Math.round((Math.random() - 0.5) * 5)
				}
			} else {
				delete particles[this.i]
			}
		}
	}

	let offsetCache = []
	for (let x = -pSpacing*8; x <=pSpacing*8; x += pSpacing){
		for (let y = -pSpacing*8; y <=pSpacing*8; y += pSpacing){
			if (x**2 + y**2 <= (pSpacing*6.2)**2) {
				offsetCache.push([x,y])
			}
		}
	}

	let genParticles = () => {
		for (const [x, y] of offsetCache) {
			new Particle(x + Math.floor(event.clientX / pSpacing) * pSpacing + 2, y + Math.floor(event.clientY / pSpacing) * pSpacing, ctx)
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