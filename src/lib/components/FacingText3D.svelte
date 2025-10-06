<script>
	import { onMount } from 'svelte';
	import Text3D from './Text3D.svelte';

	let {children, class: className = '', ...rest} = $props()

	let element;
	let rotationX = $state(0);
	let rotationY = $state(0);
	let scalar = $state(0.03)

	const handleMouseMove = (event) => {
		const rect = element.getBoundingClientRect();
		const centerX = rect.left + rect.width / 2;
		const centerY = rect.top + rect.height / 2;

		const offsetX = event.clientX - centerX;
		const offsetY = event.clientY - centerY;

		// swap because idfk man
		rotationY = offsetX * scalar;
		rotationX = -offsetY * scalar;
	};

	onMount(() => {
		window.addEventListener('mousemove', handleMouseMove);
		scalar = window.matchMedia('(prefers-reduced-motion: reduce)').matches ? 0.003 : scalar
		return () => {
			window.removeEventListener('mousemove', handleMouseMove);
		};
	});
</script>

<style>
	.rotating-box {
		transform-style: preserve-3d;
		transition: transform 0.1s ease-out;
		vertical-align: middle;
		display: inline-block;
	}
</style>

<div style="translate: 0% -100%;">
	<!-- create box unaffected by scaling -->
	<div class="invisible">
		{@render children()}
	</div>
	<div
	bind:this={element}
		class="rotating-box align-middle flex items-center justify-between"
		style="transform: rotateX({rotationX*2}deg) rotateY({rotationY*2}deg);"
	>
		<Text3D {...rest} class={className}>
			{@render children()}
		</Text3D>
	</div>
</div>