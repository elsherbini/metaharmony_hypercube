<script>
	/**
	 * Watch the video that corresponds to this code on YouTube!
	 * https://youtu.be/dnclxsoRO_E
	*/

	import {
		Canvas
	} from '@threlte/core';
	import SceneOne from '$lib/SceneOne.svelte';
	import SceneTwo from '$lib/SceneTwo.svelte';
</script>

<section>
	<h2>Scene One</h2>

	<div class="canvas-wrapper">
		<Canvas>
			<SceneOne />
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