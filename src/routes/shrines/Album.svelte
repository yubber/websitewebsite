<script>
	import { onMount } from "svelte";

	let {img, title, artist, year, backImg, slideout, class: className='', ...rest} = $props()

	let blocker, mother;

	let modalShown = $state(false);
	// $inspect(modalShown)

	let showModal = () => {
		if (!modalShown){
			modalShown = true;
			// modal?.showModal()
			doCenterMove(mother)
		}
	}

	let closeModal = (e) => {
		modalShown = false;
		backCenterMove(mother)
	}

	function calcCenterMove(element){ // https://stackoverflow.com/a/65876789

		/*
		X and Y are the current position of the element to be moved (top left corner).
		Width and Height are the width and height of the element to be moved.
		CX and CY are the X and Y coordinates of the centre of the screen.
		*/

		var x       = element.getBoundingClientRect().x;
		var y       = element.getBoundingClientRect().y;
		var width   = element.getBoundingClientRect().width;
		var height  = element.getBoundingClientRect().height;
		var cx      = window.innerWidth / 2;
		var cy      = window.innerHeight / 2;
		var xVector = cx-(width/2)-x;
		var yVector = cy-(height/2)-y;
		// console.log(xVector, yVector)
		return [xVector, yVector];
	}

	function doCenterMove(element){
		var [xAxisMove, yAxisMove] = calcCenterMove(element)
		element.style.translate = `${xAxisMove}px ${yAxisMove}px`;
	}

	function backCenterMove(element){
		element.style.translate = '';
	}

</script>

<!-- no scroll whem modal shown -->
<svelte:body class:overflow-hidden={modalShown} />
<!-- <svelte:window on:wheel|nonpassive={e => {
    if(modalShown) {e.preventDefault()}
	// else {return true}
	}
} /> -->

<div class="mother" class:modalShown={modalShown} bind:this={mother}>
	<button class="front backface-hidden" onclick={showModal}>
		<img src={img} class="object-contain backface-hidden" alt="album art for {title} by {artist}"/>
	</button>
	<modal>
		<div class="backImg">
			{@render backImg()}
		</div>
		<div class="slideout">
			{@render slideout()}
		</div>
	</modal>
</div>
<blocker onclick={closeModal}>
	<button class="absolute top-0 right-0" onclick={closeModal}>
		x
	</button>
</blocker>


<style>
	@import 'tailwindcss';

	.overflow-hidden {
		overflow: hidden;
	}

	.mother {
		-webkit-font-smoothing: subpixel-antialiased;
		transform-style: preserve-3d;
		transform: rotateX(0deg) rotateY(0deg);
		scale: 1;
		@media (prefers-reduced-motion: no-preference) {
			transition: all ease-in-out 0.4s;
		}
		/* &::hover:not(.modalShown) > button {
			cursor: pointer;
			transform: rotateX(15deg);
		} */
	}
	modal {
		/* visibility: hidden; */
		/* z-index: -10; */
		position: absolute;
		backface-visibility: hidden;
		-webkit-backface-visibility: hidden;
		width: 100%;
		height:100%;
		right: 0;
		top: 0;
		transform: rotateY(180deg);
	}
	.front {
		transform-style: preserve-3d;
		backface-visibility: hidden;
		-webkit-backface-visibility: hidden;
	}
	.slideout {
		z-index: -1;
		position: absolute;
		bottom: 5%;
		right: 1px;
		width: 50%;
		height: 90%;
		transform: translateX(0);
	}
	.backImg {
		width:100%;
		/* height:100%; */
		aspect-ratio: 1/1;
		@apply drop-shadow-lg;
	}
	.modalShown {
		z-index: 9;
		display: flex;
		justify-content: space-around;
		/* height:100vh;
		width:100vw; */
		transform: rotateY(180deg);
		scale: 1.5;
		> modal > .slideout {
			@media (prefers-reduced-motion: no-preference) {
				animation-delay: 2.5s;
				animation: ease-in-out 0.3s slideout forwards;
			}
		}
		+ blocker {
			display: block;
			position: fixed;
			width: 100vw;
			height: 100vh;
			z-index: 5;
			background: rgba(0,0,0,0.5);
			top: 0;
			left:0;
		}
	}
	blocker {
		display: none;
	}

	@keyframes slideout {
		from {transform: translateX(0);}
		to {transform: translateX(100%);}
	}
</style>