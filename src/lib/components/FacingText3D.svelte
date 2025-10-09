<script>
	import { onMount } from 'svelte';
	import Text3D from './Text3D.svelte';

	let {children, scalar=0.03, class: className = '', ...rest} = $props()

	let element;
	let rotationX = $state(0);
	let rotationY = $state(0);

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
		/* perspective-origin: 1000px; */
	}
</style>

<!-- some of the classes in the parent div are load bearing... god knows why -->
<div
bind:this={element}
	class={`rotating-box align-middle flex items-center justify-between ${className}`}
	style="transform: rotateX({rotationX*2}deg) rotateY({rotationY*2}deg);"
>
	<Text3D  {...rest}>
		{@render children()}
	</Text3D>
</div>