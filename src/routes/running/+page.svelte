<script>
	import Plotly from 'plotly.js-dist';
	import { onMount } from 'svelte';

	const runs = [
		{
			date: new Date(2023, 1, 27),
			distance: 6.22,
			duration: 64,
			activeCalories: 897,
			avgPower: 232
		},
		{
			date: new Date(2023, 1, 28),
			distance: 3.15,
			duration: 33,
			activeCalories: 470,
			avgPower: 230
		},
		{
			date: new Date(2023, 2, 2),
			distance: 3.78,
			duration: 40,
			activeCalories: 490,
			avgPower: 249
		}
	];

	/**
	 * converts str to title case
	 * example: activeCalories -> Active Calories
	 */
	function toTitleCase(str) {
		return str.replace(/([A-Z])/g, ' $1').replace(/^./, (str) => str.toUpperCase());
	}

	/**
	 * Gets the week number of the year for the given date.
	 * @returns {number} The week number.
	 */
	Date.prototype.getWeek = function () {
		const date = new Date(this.getTime());
		date.setHours(0, 0, 0, 0);
		// Thursday in current week decides the year.
		date.setDate(date.getDate() + 3 - ((date.getDay() + 6) % 7));
		// January 4 is always in week 1.
		const week1 = new Date(date.getFullYear(), 0, 4);
		// Adjust to Thursday in week 1 and count number of weeks from date to week1.
		return (
			1 +
			Math.round(
				((date.getTime() - week1.getTime()) / 86400000 - 3 + ((week1.getDay() + 6) % 7)) / 7
			)
		);
	};

	/**
	 * Aggregates the runs by week (totals distance and duration over the week).
	 * @param runs The runs to aggregate.
	 */
	function aggregateByWeek(runs) {
		const weeks = new Map();
		for (const run of runs) {
			const week = run.date.getWeek();
			if (!weeks.has(week)) {
				weeks.set(week, {
					date: run.date,
					distance: 0,
					duration: 0,
					activeCalories: 0,
					averagePower: null
				});
			}
			const weekData = weeks.get(week);
			weekData.distance += run.distance;
			weekData.duration += run.duration / 60;
			weekData.activeCalories += run.activeCalories;
			if (weekData.averagePower === null) {
				weekData.averagePower = run.avgPower;
			} else {
				weekData.averagePower = (weekData.averagePower + run.avgPower) / 2;
			}
		}
		return weeks;
	}

	const weeks = aggregateByWeek(runs);
	const metrics = ['distance', 'duration', 'activeCalories', 'averagePower'];
	const precisions = { distance: 4, duration: 2, activeCalories: 4, averagePower: 3 };
	const axisLabels = {
		distance: 'Distance (mi)',
		duration: 'Duration (hr)',
		activeCalories: 'Calories (kcal)',
		averagePower: 'Average Power (W)'
	};
	const generalLayout = {
		plot_bgcolor: '#18181b',
		paper_bgcolor: '#18181b',
		font: { color: '#e4e4e7' },
		margin: { l: 55, r: 10, pad: 5 }
	};
	const config = {
		responsive: true,
		displayModeBar: false
	};
	const data = {};
	const layout = {};
	metrics.forEach((metric) => {
		data[metric] = [
			{
				x: Array.from(weeks.values()).map((week) => week.date),
				y: Array.from(weeks.values()).map((week) => week[metric].toPrecision(precisions[metric])),
				type: 'scatter',
				mode: 'lines+markers'
			}
		];
		layout[metric] = {
			...generalLayout,
			title: toTitleCase(metric),
			xaxis: { title: 'Date' },
			yaxis: { title: axisLabels[metric] }
		};
	});

	onMount(() => {
		metrics.forEach((metric) => {
			Plotly.newPlot(metric, data[metric], layout[metric], config);
		});
	});
</script>

<svelte:head>
	<title>Running - Collin Sinclair</title>
	<meta name="description" content="A page that displays my running data and trends." />
</svelte:head>

<main class="container">
	<h1 class="text-3xl text-zinc-200 py-3">Running</h1>
	<div class="grid grid-cols-1 lg:grid-cols-4">
		{#each metrics as metric}
			<div id={metric} />
		{/each}
	</div>
</main>
