<script>
	let { layers=8, gapPx=2, brightnessDrop=null, class: className = '', firstZ=0, children, ...rest } = $props();
	if (brightnessDrop === null){
		brightnessDrop = 80/layers;
	}
</script>

<div class={`container3d ${className}`}>
	<!-- make invisible element with a box -->
	<div class="invisible">
		{@render children()}
	</div>
	{#each [...Array(layers).keys()] as i (i)}
		<div
			class={className}
			style="
				transform: translateZ({firstZ - (i) * gapPx}px);
				filter: brightness({Math.max(0,100-i*brightnessDrop)}%);
			"
		>
			{@render children()}
		</div>
	{/each}
</div>

<style>
	.container3d{
		display: inline-block;
		transform-style: preserve-3d;
		width: fit-content;
		text-align: center;
		backface-visibility: visible;
		white-space: normal;

		> div:first-child {
			position: relative;
			margin: 0 auto;
			text-align: center;
			width: fit-content;
		}
		> div:not(:first-child) {
			inset: 0;
			position: absolute;
			width: fit-content;
			height: fit-content;
		}
		> div {
			text-align: center;
		}
	}

</style>