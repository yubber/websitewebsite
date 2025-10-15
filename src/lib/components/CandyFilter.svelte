<script>
	let {animateDuration=0} = $props()
</script>

<svg>
	<filter id="candy" color-interpolation-filters="sRGB" filterUnits="objectBoundingBox" primitiveUnits="userSpaceOnUse">
		<feTurbulence type="turbulence" baseFrequency="0.015 0.1" numOctaves="2" seed="2" stitchTiles="stitch" x="0" y="0%" width="100%" height="100%" result="turbulence"/>
		{#if animateDuration > 0}
			<animate attributeName="x" from="0" to="100" dur="{animateDuration}s" repeatCount="indefinite"/>
		{/if}
	</filter>
</svg>