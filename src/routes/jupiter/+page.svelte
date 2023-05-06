<script>
	import jupiterImage from '$lib/img/jupiter.jpeg';
	import Plotly from 'plotly.js-dist';
	import { onMount } from 'svelte';

	const weights = [
		4.5, 4.6, 5.1, 5.4, 6.7, 6.9, 7, 7.2, 7.6, 7.6, 7.8, 7.9, 8.1, 8.2, 8.3, 8.7, 9.1, 9.4, 9.8,
		9.8, 10.3, 10.7, 11, 11.5, 11.7, 12.5, 12.8
	];
	const dates = [
		'2022-11-30',
		'2022-12-03',
		'2022-12-06',
		'2022-12-09',
		'2022-12-28',
		'2022-12-29',
		'2022-12-31',
		'2023-01-02',
		'2023-01-05',
		'2023-01-07',
		'2023-01-09',
		'2023-01-11',
		'2023-01-16',
		'2023-01-19',
		'2023-01-25',
		'2023-01-28',
		'2023-02-01',
		'2023-02-06',
		'2023-02-09',
		'2023-02-19',
		'2023-02-26',
		'2023-03-02',
		'2023-03-08',
		'2023-03-24',
		'2023-03-28',
		'2023-04-19',
		'2023-05-06'
	];
	const axisLabels = ['Date', 'Weight (lbs)'];
	const birthday = new Date('2022-08-08');
	const monthsOld = new Date(new Date() - birthday).getMonth();
	const data = [
		{
			x: dates,
			y: weights,
			type: 'scatter',
			mode: 'lines',
			line: { shape: 'spline' }
		}
	];
	const layout = {
		title: 'Weight',
		xaxis: { title: axisLabels[0] },
		yaxis: { title: axisLabels[1] },
		plot_bgcolor: '#18181b',
		paper_bgcolor: '#18181b',
		font: { color: '#e4e4e7' },
		margin: { l: 40, r: 10 }
	};
	const config = { responsive: true, displayModeBar: false };
	onMount(() => {
		Plotly.newPlot('plot', data, layout, config);
	});
</script>

<svelte:head>
	<title>Jupiter - Collin Sinclair</title>
	<meta name="description" content="Jupiter is Collin's red tabby Maine coon cat." />
</svelte:head>
<main class="container">
	<h1 class="text-zinc-200 text-3xl py-3">Jupiter</h1>
	<p class="text-zinc-200 text-justify">
		Jupiter is a red tabby Maine coon whom Gabrielle and I adopted in November 2022. The joy that he
		brings into our lives is beyond measure and constant, every minute of every day. He is {monthsOld}
		months old.
	</p>
	<div class="max-w-md mx-auto my-3">
		<img
			src={jupiterImage}
			alt="A red tabby Maine coon sitting on a bed."
			class="rounded-lg"
			width="960"
			height="1280"
		/>
	</div>
	<div id="plot" />
</main>
