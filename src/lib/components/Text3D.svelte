<script>
	let { layers=8, gapPx=2, RGB=[220,220,220], lumDrop=0.0055, class: className = '', children, ...rest } = $props();

	// avoid errors in native conversion??
	function rgbLuminanceDrop(rgb, luminanceDrop) {
		// sRGB to linear light
		function srgbToLinear(c) {
			c /= 255;
			return c <= 0.04045
			? c / 12.92
			: Math.pow((c + 0.055) / 1.055, 2.4);
		}

		// Linear light to sRGB
		function linearToSrgb(c) {
			return c <= 0.0031308
			? c * 12.92
			: 1.055 * Math.pow(c, 1 / 2.4) - 0.055;
		}

		// Relative luminance weights (sRGB)
		const LUMA = [0.2126, 0.7152, 0.0722];

		// Convert to linear RGB
		const linearRGB = rgb.map(e => srgbToLinear(e));

		// Compute current luminance
		const currentLuminance = linearRGB.reduce((sum, c, i) => sum + c * LUMA[i], 0);

		// Compute target luminance
		const targetLuminance = Math.max(0, currentLuminance - luminanceDrop);

		// If luminance is zero or color is black, return black
		if (currentLuminance === 0 || targetLuminance === 0) {
			return '#000000';
		}

		// Scale factor to reach target luminance
		const scale = targetLuminance / currentLuminance;

		// Scale each linear RGB channel
		const newLinearRGB = linearRGB.map(c => c * scale);

		// Convert back to sRGB
		const newSRGB = newLinearRGB.map(c =>
			Math.round(Math.min(255, Math.max(0, linearToSrgb(c) * 255)))
		);

		// Convert to hex
		const hex = newSRGB
			.map(c => c.toString(16).padStart(2, '0'))
			.join('').toUpperCase()
		return `#${hex}`;
	}
</script>

<div class={`container3d ${className}`}>
	<!-- make invisible element with a box -->
	<div class="invisible">
		{@render children()}
	</div>
	{#each [...Array(layers).keys()] as i}
		<div
			style="
				transform: translateZ({-i * gapPx}px);
				color: {rgbLuminanceDrop(RGB, lumDrop * i)};
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
		white-space: nowrap;

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
			white-space: nowrap;
		}
		> div {
			text-align: center;
		}
	}

</style>