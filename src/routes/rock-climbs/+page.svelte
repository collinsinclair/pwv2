<script lang="ts">
	import * as am5 from '@amcharts/amcharts5';
	import am5themes_Animated from '@amcharts/amcharts5/themes/Animated';
	import * as am5hierarchy from '@amcharts/amcharts5/hierarchy';
	import csvData from './rock-climbs.json';
	import { onMount } from 'svelte';
	function parseCSVData(data) {
		const treeData = {};
		data.forEach((item) => {
			const locationPath = item['Location'];
			const locationParts = locationPath.split(' > ').reverse();
			let currentLevel = treeData;
			locationParts.forEach((part, index) => {
				if (!currentLevel[part]) {
					currentLevel[part] = {
						name: part,
						children: index === locationParts.length - 1 ? [] : {}
					};
				}
				if (index === locationParts.length - 1) {
					currentLevel[part].value = (currentLevel[part].value || 0) + 1;
				} else {
					currentLevel = currentLevel[part].children;
				}
			});
		});
		function convertToNestedArray(obj) {
			return Object.values(obj).map((item) => {
				if (item.children) {
					item.children = convertToNestedArray(item.children);
				}
				return item;
			});
		}
		return convertToNestedArray(treeData);
	}
	const hierarchyData = parseCSVData(csvData);
	onMount(() => {
		let root = am5.Root.new('chartdiv');
		const myTheme = am5.Theme.new(root);
		// myTheme.rule('RoundedRectangle', ['hierarchy', 'node', 'shape', 'depth1']).setAll({
		// 	strokeWidth: 2
		// });
		// myTheme.rule('RoundedRectangle', ['hierarchy', 'node', 'shape', 'depth2']).setAll({
		// 	fillOpacity: 0,
		// 	strokeWidth: 1,
		// 	strokeOpacity: 0.2
		// });
		// myTheme.rule('Label', ['node', 'depth1']).setAll({
		// 	forceHidden: true
		// });
		// myTheme.rule('Label', ['node', 'depth2']).setAll({
		// 	fontSize: 10
		// });
		root.setThemes([am5themes_Animated.new(root), myTheme]);
		let container = root.container.children.push(
			am5.Container.new(root, {
				width: am5.percent(100),
				height: am5.percent(100),
				layout: root.verticalLayout
			})
		);
		let series = container.children.push(
			am5hierarchy.Treemap.new(root, {
				sort: 'descending',
				singleBranchOnly: false,
				downDepth: 1,
				upDepth: 0,
				initialDepth: 1,
				valueField: 'value',
				categoryField: 'name',
				childDataField: 'children',
				nodePaddingOuter: 0,
				nodePaddingInner: 0
			})
		);
		series.get('colors').set('step', 1);
		container.children.moveValue(
			am5hierarchy.BreadcrumbBar.new(root, {
				series: series
			}),
			0
		);
		series.data.setAll(hierarchyData);
		series.set('selectedDataItem', series.dataItems[0]);
	});
</script>

<main class="container">
	<h1 class="text-zinc-200 text-3xl py-3">Rock Climbs</h1>
	<p class="text-zinc-200 text-justify">
		Rock routes (Sport or Toprope) in Colorado between 5.0 and 5.9+ with at least 3 stars and
		exactly 1 pitch.
	</p>
	<div id="chartdiv" class="w-full aspect-video" />
</main>
