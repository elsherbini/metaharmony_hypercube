<script>
	/**
	 * Watch the video that corresponds to this code on YouTube!
	 * https://youtu.be/dnclxsoRO_E
	*/

	import {
		Canvas
	} from '@threlte/core';
	import Hypercube from '$lib/Hypercube.svelte';
</script>

<section>
	<h2>Hypercube</h2>

	<div class="canvas-wrapper">
		<Canvas>
			<Hypercube root=C/>
		</Canvas>
	</div>

</section>

<style>
	.canvas-wrapper {
		position: relative;
		/* border: 1px solid black; */
		height: 600px;
	}
</style>