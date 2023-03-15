<script>
	import { Map, Marker, controls } from '@beyonk/svelte-mapbox';
	import { onMount } from 'svelte';
	import coSummitClimbs from '$lib/json/colorado-summit-hikes.json';

	let mapComponent;
	const { GeolocateControl, NavigationControl } = controls;
	const accessToken =
		'pk.eyJ1IjoiY29sbGluc2luY2xhaXIiLCJhIjoiY2w4dnl3b2U4MGlvbTNvc3Jna3I0cml4byJ9.GXhvyfjGlngMo7MpNEkMRA';
	const style = 'mapbox://styles/mapbox/outdoors-v12';
	const colors = ['green', 'blue'];

	let maxElevation = 14000;
	let minElevation =
		Math.floor(Math.min(...coSummitClimbs.map((climb) => climb['Elevation'])) / 100) * 100;
	let elevationFilter = minElevation;
	let difficulties = [0, 1, 2, 3];

	$: filteredClimbs = coSummitClimbs.filter((climb) => {
		return climb['Elevation'] >= elevationFilter && difficulties.includes(climb['Difficulty']);
	});

	onMount(() => {
		mapComponent.setCenter([-104.99028, 39.73925], 10);
	});

	$: console.log(difficulties);
</script>

<svelte:head>
	<script src="https://api.mapbox.com/mapbox-gl-js/v2.13.0/mapbox-gl.js"></script>
	<link href="https://api.mapbox.com/mapbox-gl-js/v2.13.0/mapbox-gl.css" rel="stylesheet" />
</svelte:head>
<div class="container columns-1 lg:columns-2">
	<h1 class="text-zinc-200 text-3xl py-3">Map</h1>
	<p class="text-zinc-200">
		Right now the map shows summit climbs in Colorado. Eventually I will add more data sets to
		include snow climbs, trail runs, and other outdoor endeavors.
	</p>
	<hr class="my-2" />
	<div class="w-full aspect-auto mb-3">
		<label class="text-zinc-200"
			>Show summits above: {elevationFilter.toLocaleString()} feet
			<input
				type="range"
				bind:value={elevationFilter}
				min={minElevation}
				max={maxElevation}
				step="500"
				class="w-full"
			/>
		</label>
		<button
			class="rounded bg-zinc-200 text-zinc-800 w-full my-1.5 block"
			on:click={() => (elevationFilter = 11500)}
		>
			<span class="block lg:inline font-bold">Above Tree Line</span> (>11,500 feet)
		</button>
		<button
			class="rounded bg-zinc-200 text-zinc-800 w-full my-1.5 block"
			on:click={() => (elevationFilter = 13000)}
		>
			<span class="block lg:inline font-bold">13ers</span> (>13,000 feet)
		</button>
		<button
			class="rounded bg-zinc-200 text-zinc-800 w-full my-1.5 block"
			on:click={() => (elevationFilter = 14000)}
		>
			<span class="block lg:inline font-bold">14ers</span> (>14,000 feet)
		</button>
		<label class="text-zinc-200 block lg:inline">
			Show climbs that are
			<div class="block lg:inline">
				<input type="checkbox" bind:group={difficulties} value={0} />
				<span class="text-green-500">easy</span>
			</div>
			<div class="block lg:inline">
				<input type="checkbox" bind:group={difficulties} value={1} />
				<span class="text-blue-500">moderate</span>
			</div>
			<div class="block lg:inline">
				<input type="checkbox" bind:group={difficulties} value={2} />
				<span class="text-yellow-500">hard</span>
			</div>
			<div class="block lg:inline">
				<input type="checkbox" bind:group={difficulties} value={3} />
				<span class="text-red-500">extreme</span>
			</div>
		</label>
	</div>
	<div class="w-full aspect-square">
		<Map {accessToken} bind:this={mapComponent} {style}>
			<GeolocateControl />
			<NavigationControl />
			{#each filteredClimbs as climb}
				<Marker
					lat={climb['Latitude']}
					lng={climb['Longitude']}
					label={climb.Name}
					color={colors[climb['Difficulty']]}
				/>
			{/each}
		</Map>
	</div>
</div>

<style>
	:global(.mapboxgl-map) {
		/*min-height: 85vh;*/
	}
</style>
