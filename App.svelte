<script lang="ts">
	import Column from './Column.svelte';
	import { onMount } from 'svelte';

	let matrix;
	let numberOfColumns = 200;
	let charWidth;

	let columns = [];

	onMount(() => {
		const containerWidth = matrix.offsetWidth;
		const containerHeight = matrix.offsetHeight;
		charWidth = containerWidth / numberOfColumns;
		
		for (let i = 0; i < numberOfColumns; i++) {
			columns.push({
				x: containerWidth / numberOfColumns * Math.floor(Math.random() * numberOfColumns),
				y: (Math.random() - 0.3) * containerHeight,
				z: Math.random()
			});
		}

		setInterval(() => {
			columns.shift();
			columns = [...columns, {
				x: Math.min(Math.random() * containerWidth, containerWidth - charWidth),
				y: (Math.random() - 0.3) * containerHeight,
				z: Math.random()
			}];
		}, 100);
	});
</script>

<div bind:this={matrix} style="overflow: hidden; background-color: black; width: 100%; height: 100%; position: relative; padding-right: 10px; margin-right: 10px">
	{#each columns as column (column.z)}
		<Column {column} width={charWidth} />
	{/each}
</div>
