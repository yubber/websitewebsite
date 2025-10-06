<script>
	import Text3D from "./Text3D.svelte";
	let { layers=8, gapPx=2, brightnessDrop=null, class: className = '', children, ...rest } = $props();
</script>

<div class="spincontainer">
	<Text3D {layers} {gapPx} {brightnessDrop} {...rest} class={className}>
		{@render children()}
	</Text3D>
</div>

<style>
	.spincontainer {
		transform: rotateY(0deg);
		animation-name: spinner;
		animation-timing-function: linear;
		animation-iteration-count: infinite;
		@media (prefers-reduced-motion: no-preference) {
			animation-duration: 4s;
		}
		@media (prefers-reduced-motion: reduce) {
			animation-duration: 40s;
		}
		/* width: 100%; */
		display: flex;
		justify-content: space-around;
		height: auto;
		transform-style: preserve-3d;
	}

	@keyframes spinner {
		from {
			transform: rotateY(0deg);
		}
		to {
			transform: rotateY(-360deg);
		}
	}
</style>