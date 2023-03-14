<script>
	import { Map, Marker, controls } from '@beyonk/svelte-mapbox';
	import { onMount } from 'svelte';
	import coSummitClimbs from '$lib/json/colorado-summit-hikes.json';

	console.log(coSummitClimbs);
	let mapComponent;
	const { GeolocateControl, NavigationControl, ScaleControl } = controls;
	const accessToken =
		'pk.eyJ1IjoiY29sbGluc2luY2xhaXIiLCJhIjoiY2w4dnl3b2U4MGlvbTNvc3Jna3I0cml4byJ9.GXhvyfjGlngMo7MpNEkMRA';
	const style = 'mapbox://styles/mapbox/outdoors-v12';
	const colors = ['green', 'blue'];
	onMount(() => {
		mapComponent.setCenter([-104.99028, 39.73925], 10);
	});
</script>

<svelte:head>
	<script src="https://api.mapbox.com/mapbox-gl-js/v2.13.0/mapbox-gl.js"></script>
	<link href="https://api.mapbox.com/mapbox-gl-js/v2.13.0/mapbox-gl.css" rel="stylesheet" />
</svelte:head>
<div class="mx-1 mx-auto my-auto">
	<Map {accessToken} bind:this={mapComponent} {style}>
		<GeolocateControl />
		<NavigationControl />
		{#each coSummitClimbs as climb}
			<Marker
				lat={climb['Latitude']}
				lng={climb['Longitude']}
				label={climb.Name}
				color={colors[climb['Difficulty']]}
			/>
		{/each}
	</Map>
</div>

<style>
	:global(.mapboxgl-map) {
		min-height: 85vh;
	}
</style>
