<script>
	import { Map, Marker, controls } from '@beyonk/svelte-mapbox';
	import { onMount } from 'svelte';
	import coSummitClimbs from '$lib/json/colorado-summit-hikes.json';

	let mapComponent;
	const { GeolocateControl, NavigationControl } = controls;
	const accessToken =
		'pk.eyJ1IjoiY29sbGluc2luY2xhaXIiLCJhIjoiY2w4dnl3b2U4MGlvbTNvc3Jna3I0cml4byJ9.GXhvyfjGlngMo7MpNEkMRA';
	const style = 'mapbox://styles/mapbox/outdoors-v12';
	let maxElevation = 14000;
	let minElevation =
		Math.floor(Math.min(...coSummitClimbs.map((climb) => climb['Elevation'])) / 100) * 100;
	let elevationFilter = minElevation;
	let difficulty = 0;
	function getColor(difficulty) {
		switch (difficulty) {
			case 0:
				return 'green';
			case 1:
				return 'blue';
			case 2:
				return 'orange';
			case 3:
				return 'red';
		}
	}
	const filterClimbs = () => coSummitClimbs.filter((climb) => {
		return climb['Elevation'] >= elevationFilter && climb['Difficulty'] === difficulty;
	});

	let filteredClimbs = filterClimbs();

	$: {
		if (difficulty !== null && elevationFilter !== null) {
			filteredClimbs = filterClimbs();
			if (filteredClimbs.length > 0 && mapComponent) {
				centerMapToClimbs(filteredClimbs);
			}
		}
	}

	function centerMapToClimbs(climbs) {
		const totalLocation = climbs.reduce((total, climb) => {
			return {
				lat: total.lat + climb['Latitude'],
				lng: total.lng + climb['Longitude']
			};
		}, {lat: 0, lng: 0});

		const avgLocation = {
			lat: totalLocation.lat / climbs.length,
			lng: totalLocation.lng / climbs.length
		};

		mapComponent.setCenter([avgLocation.lng, avgLocation.lat]);
	}
	onMount(() => {
		mapComponent.setCenter([-104.99028, 39.73925], 10);
	});
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
	<div class="w-full aspect-auto">
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
		<p class="text-zinc-200">Show climbs that are</p>
		<div class="block lg:inline">
			<input type="radio" bind:group={difficulty} value={0} />
			<span class="text-green-500">easy</span>
		</div>
		<div class="block lg:inline">
			<input type="radio" bind:group={difficulty} value={1} />
			<span class="text-blue-500">moderate</span>
		</div>
		<div class="block lg:inline">
			<input type="radio" bind:group={difficulty} value={2} />
			<span class="text-yellow-500">hard</span>
		</div>
		<div class="block lg:inline">
			<input type="radio" bind:group={difficulty} value={3} />
			<span class="text-red-500">extreme</span>
		</div>
	</div>
	<div class="w-full aspect-square pt-3">
		<Map {accessToken} bind:this={mapComponent} {style}>
			<GeolocateControl />
			<NavigationControl />
			{#each filteredClimbs as climb (`${climb.Name}-${climb.Elevation}`)}
				<Marker
					lat={climb['Latitude']}
					lng={climb['Longitude']}
					label={`${climb.Name} (${climb['Elevation'].toLocaleString()} ft)`}
					color={getColor(climb['Difficulty'])}
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
