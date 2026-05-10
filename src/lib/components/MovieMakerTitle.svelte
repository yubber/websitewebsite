<script>
	let {children} = $props()
</script>

<div id="outer">
	<div>
		<h1>
			{@render children()}
		</h1>
		<span id="float1">
			{@render children()}
		</span>
		<span id="float2">
			{@render children()}
		</span>
	</div>
</div>

<style>
	#outer {
		position: relative;
		height: 100%;
		width: 100%;
		background-color: #4f86af;
		color: var(--color-blue-100);
		font-size: var(--text-4xl);
		overflow: hidden;
	}
	#outer > div > * {
		user-select: none;
		cursor: default;
		font-family: "Comic Sans MS", cursive;
		position: absolute;
		transform: translate(-50%, -50%);
	}
	h1 {
		top: 50%;
		left: 50%;
	}
	span {
		white-space: nowrap;
	}
	#float1 {
		top: 45%;
		font-size: var(--text-5xl);
		animation: drift1 25s infinite;
	}
	#float2 {
		font-size: var(--text-8xl);
		top: 55%;
		opacity: 30%;
		animation: drift2 30s infinite;
	}

	@keyframes drift1 {
		0% {
			left: 30%;
			opacity: 0%;
		}
		30% {
			opacity: 50%
		}
		70% {
			opacity: 50%
		}
		100% {
			left: 80%;
			opacity: 0%;
		}
	}
	@keyframes drift2 {
		0% {
			left: 100%;
			opacity: 0%;
		}
		30% {
			opacity: 30%
		}
		70% {
			opacity: 30%
		}
		100% {
			left: 40%;
			opacity: 0%;
		}
	}
</style>