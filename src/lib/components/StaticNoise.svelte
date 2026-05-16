<script>
	let {className = ''} = $props()
</script>

<div class={className}></div>

<style>
	div {
		height: 100%;
		width: 100%;
		background-image: repeating-radial-gradient(circle at 17% 32%, white, black 0.00085px);
		background-position: center;
		animation: back 5s linear infinite;
	}

	@keyframes back {
		from {
			background-size: 100% 100%;
		}
		to {
			background-size: 200% 200%;
		}
	}
</style>