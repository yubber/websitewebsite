<script>
	import SpinText from "$lib/components/SpinText.svelte";
	import GlitchText from "$lib/components/GlitchText.svelte";
</script>


<div class="flex place-content-center flex-col h-svh">
	<SpinText class="stretchroman text-9xl mb-8" RGB={[0,0,206]}>yubz' website</SpinText>

	<div class="flex place-items-center items-start font-mono text-gray-100 lowercase justify-around w-full text-2xl">
		<div>
			<!-- maybe enable peer hover + -->
			<GlitchText class="peer">
				<span>projects</span>
			</GlitchText>
			<div class="text-m flex flex-col glow transition-all ease-in peer-hover:translate-y-0 translate-y-9 opacity-0 peer-hover:opacity-70">
				<a href="#">code</a>
				<a href="#">videos</a>
				<a href="#">misc</a>
			</div>
		</div>
		<GlitchText class="hovergrow">
			<a href="">accolades</a>
		</GlitchText>
		<GlitchText class="hovergrow">
			<a href="">my rabbit</a>
		</GlitchText>
		<GlitchText class="hovergrow">
			<a href="">about</a>
		</GlitchText>
		<GlitchText class="hovergrow">
			<a href="">contact</a>
		</GlitchText>
	</div>
</div>

