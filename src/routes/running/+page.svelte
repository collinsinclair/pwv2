<script>
	import Plotly from 'plotly.js-dist';

	const runs = [{ date: new Date(), distance: 0.0, duration: 0 }];

	/**
	 * Aggregates the runs by week (totals distance and duration over the week).
	 * @param runs The runs to aggregate.
	 */
	function aggregateByWeek(runs) {
		const weeks = new Map();
		for (const run of runs) {
			const week = run.date.getWeek();
			if (!weeks.has(week)) {
				weeks.set(week, { distance: 0, duration: 0 });
			}
			const weekData = weeks.get(week);
			weekData.distance += run.distance;
			weekData.duration += run.duration;
		}
		return weeks;
	}
</script>

<svelte:head>
	<title>Running - Collin Sinclair</title>
	<meta name="description" content="A page that displays my running data and trends." />
</svelte:head>

<main class="container">
	<h1 class="text-3xl text-zinc-200 py-3">Running</h1>
</main>
