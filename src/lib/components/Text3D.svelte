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
	{#each [...Array(layers).keys()] as i}
		<div
			class={className}
			style="
				transform: translateZ({firstZ -i * gapPx}px);
				filter: brightness({100-i*brightnessDrop}%);
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
		/*load bearing*/
		/* width:100%; */
		text-align: center;
		/* white-space: nowrap; */

		> div:first-child {
			position: relative;
			margin: 0 auto;
			text-align: center;
			width: fit-content;
			/* background-color: fuchsia; */
		}
		> div:not(:first-child) {
			left: 0%;
			bottom: 0;
			/* transform: translate(-200%, 0); */
			position: absolute;
			width: fit-content;
			/* white-space: nowrap; */
		}
		> div {
			text-align: center;
		}
	}

</style>