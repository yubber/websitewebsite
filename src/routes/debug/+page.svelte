<script>
	import { onMount } from "svelte";
	import SpinText from "$lib/components/SpinText.svelte";

	var canvas;
	onMount(()=>{
		const gl = canvas.getContext("webgl");
		gl.clear(gl.COLOR_BUFFER_BIT);
		canvas.width = window.innerWidth * window.devicePixelRatio
		canvas.height = window.innerHeight * window.devicePixelRatio

		const resizeHandler = () => {
			canvas.width = window.innerWidth * window.devicePixelRatio;
			canvas.height = window.innerHeight * window.devicePixelRatio;
		}
		window.addEventListener('resize', resizeHandler)

		// Vertex shader program
		const vsSource = `
			attribute vec4 aVertexPosition;
			uniform mat4 uModelViewMatrix;
			uniform mat4 uProjectionMatrix;
			void main() {
			gl_Position = uProjectionMatrix * uModelViewMatrix * aVertexPosition;
			}
		`;

		const fsSource = `
			void main() {
			gl_FragColor = vec4(1.0, 1.0, 1.0, 1.0);
			}
		`;

		//
		// Initialize a shader program, so WebGL knows how to draw our data
		//
		function initShaderProgram(gl, vsSource, fsSource) {
			const vertexShader = loadShader(gl, gl.VERTEX_SHADER, vsSource);
			const fragmentShader = loadShader(gl, gl.FRAGMENT_SHADER, fsSource);

			// Create the shader program

			const shaderProgram = gl.createProgram();
			gl.attachShader(shaderProgram, vertexShader);
			gl.attachShader(shaderProgram, fragmentShader);
			gl.linkProgram(shaderProgram);

			// If creating the shader program failed, alert

			if (!gl.getProgramParameter(shaderProgram, gl.LINK_STATUS)) {
				alert(
				`Unable to initialize the shader program: ${gl.getProgramInfoLog(
					shaderProgram,
					)}`,
					);
					return null;
				}

				return shaderProgram;
			}

			//
			// creates a shader of the given type, uploads the source and
			// compiles it.
			//
			function loadShader(gl, type, source) {
				const shader = gl.createShader(type);

				// Send the source to the shader object

				gl.shaderSource(shader, source);

				// Compile the shader program

				gl.compileShader(shader);

				// See if it compiled successfully

				if (!gl.getShaderParameter(shader, gl.COMPILE_STATUS)) {
					alert(
					`An error occurred compiling the shaders: ${gl.getShaderInfoLog(shader)}`,
					);
					gl.deleteShader(shader);
					return null;
				}

				return shader;
			}
		})
	</script>

	<svelte:head>
	<script src="https://cdnjs.cloudflare.com/ajax/libs/gl-matrix/2.8.1/gl-matrix-min.js"
	integrity="sha512-zhHQR0/H5SEBL3Wn6yYSaTTZej12z0hVZKOv3TwCUXT1z5qeqGcXJLLrbERYRScEDDpYIJhPC1fk31gqR783iQ=="
	crossorigin="anonymous"
	defer></script>
</svelte:head>

<pre>
	testt testset setst
</pre>
<div class="stretchroman">
	<SpinText class="text-[10rem] text-[#8ace00] cursor-default">i've got a song that nobody knows</SpinText>
</div>
<canvas bind:this={canvas}></canvas>