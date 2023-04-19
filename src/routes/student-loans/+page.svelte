<script>
	import Plotly from 'plotly.js-dist';
	import { onMount } from 'svelte';

	const payments = [
		4334.49, 4237.96, 2300, 1405.99, 1000, 3084.83, 5731, 18.39, 5000, 3000, 3247.28
	];
	const dates = [
		new Date(2022, 6, 31),
		new Date(2022, 8, 2),
		new Date(2022, 9, 4),
		new Date(2022, 9, 24),
		new Date(2022, 10, 4),
		new Date(2022, 11, 5),
		new Date(2023, 0, 13),
		new Date(2023, 0, 20),
		new Date(2023, 1, 22),
		new Date(2023, 2, 24),
		new Date(2023, 3, 18)
	];
	let cumSum = 0;
	const cumSumPayments = payments.map((payment) => {
		cumSum += payment;
		return cumSum;
	});
	const data = [
		{ x: dates, y: cumSumPayments, type: 'scatter', mode: 'lines', line: { shape: 'spline' } }
	];
	const layout = {
		title: 'Cumulative Sum of Repayments',
		xaxis: { title: 'Date' },
		yaxis: { title: 'Dollars (USD)' },
		plot_bgcolor: '#18181b',
		paper_bgcolor: '#18181b',
		font: { color: '#e4e4e7' },
		margin: { l: 55, r: 10, pad: 5 }
	};
	const config = { responsive: true, displayModeBar: false };
	onMount(() => {
		Plotly.newPlot('plot', data, layout, config);
	});
</script>

<svelte:head>
	<title>Student Loans - Collin Sinclair</title>
	<meta name="description" content="A plot of my student loans paid over time." />
</svelte:head>

<main class="container">
	<h1 class="text-zinc-200 text-3xl py-3">Student Loans</h1>
	<p class="text-zinc-200 text-justify">
		Here I plot my student loan repayments over time. So far, I have repaid ${Math.round(
			cumSumPayments.at(-1)
		).toLocaleString()}.
	</p>
	<div id="plot" />
</main>
