<script>
	import '../app.css';
	import favicon from '$lib/assets/favicon.png';
	import girledm from '$lib/assets/girledm fairy.png';

	let { children } = $props();

	let x = $state();
	let y = $state();

	function handleMousemove(event) {
		x = event.clientX;
		y = event.clientY;
	}
</script>

<svelte:head>
<link rel="icon" href={favicon} />
</svelte:head>

{@render children?.()}

<svelte:window on:mousemove={handleMousemove}/>

<div
  id="cursorfollow"
  style="transform: translate({x}px, {y}px); mix-blend-mode: exclusion;"
>
	<img src={girledm} alt="" srcset="">
</div>

<style>
	* {
		font-family: Arial, Helvetica, sans-serif;
	}

  #cursorfollow {
    position: fixed;
    top: 0;
    left: 0;
    width: 50px;
    height: 50px;
    pointer-events: none; /* Prevents flickering */
    margin-top: 15px;
    margin-left: 10px;
  }
</style>
