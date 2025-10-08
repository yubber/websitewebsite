<script>
	let {img, title, artist, year, children, class: className='', ...rest} = $props()
</script>

<div class={`mother h-full w-full ${className}`} {...rest} tabindex="0">
	<img src={img} class="object-contain" alt="album art for {title} by {artist}"/>
	<div class="popout">
		{@render children()}
		<p class="text-gray-600 p-4">{title} by {artist} ({year})</p>
	</div>
</div>

<style>
	div.mother:hover, div.mother:focus, div.mother:focus-within {
		img {
			transform: scale(1.1);
		}
		> div.popout {
			/* can't transition to h auto */
			max-height: 100lvh;
		}
	}
	div.popout {
		z-index: -10;
		max-height: 0;
		transition: all 150ms ease-in-out;
		animation-direction: alternate;
		overflow:hidden;
	}
	img {
		transform:scale(1);
		transition-duration: 150ms;
		transition-property: all;
		animation-direction: alternate;
		transition-timing-function: ease-out;
	}
</style>