<script lang="ts">
	import { fade } from 'svelte/transition';
	import { onMount } from 'svelte';

	export let column;
	export let width;

	const chars = `丹日亡句ヨ乍呂廾工勹片し冊几回尸甲尺己卞凵レ山メと乙!@#$%^&*()/[]1234567890`;

	let text = '';

	const numberOfMiliSecondsToRun = Math.random() * 10 * 1000;
	const startDate = new Date();
	let isDone = false;

	onMount(() => {
		const intervalId = setInterval(() => {
			const now = new Date();
			if (now.getTime() > startDate.getTime() + numberOfMiliSecondsToRun) {
				isDone = true;
				clearInterval(intervalId);
				return;
			}

			requestAnimationFrame(() => {
				text += chars[Math.ceil(Math.random() * chars.length) - 1];
				
			});
		}, 150);
	});
</script>

<div
		 style="position: absolute; width: {width / 2}px; top: {column.y}px; left: {column.x}px;display: flex; flex-direction: column; justify-items: center; color: rgb(26, 182, 29);
						word-break: break-all; transform: rotateY(180deg) scale({column.z}); opacity: {column.z}; z-index: {column.z * 100} width: 1px; line-height: 1.2; font-variant-ligatures: no-common-ligatures;"
		 transition:fade>
	{#each text.substring(0, text.length - 3) as char}
	<span>{char}</span>
	{/each}

	<span class="shadow {isDone ? '' : 'animated'}">
		{text.substr(text.length - 2, 1)}
	</span>
	<span class="shadow {isDone ? '' : 'animated'} last">
		{text.substr(text.length - 1, 1)}
	</span>
</div>

<style>
	.shadow.animated {
		text-shadow: #1fc 1px 0 10px;
		font-weight: 600;
	}
	.shadow.animated.last {
		color: white;
	}
</style>
