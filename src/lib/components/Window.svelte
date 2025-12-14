<script lang="ts">
	import { onMount } from 'svelte';

	export let title: string = '';

	let isDragging = false;
	let currentX = 0;
	let currentY = 0;
	let initialX = 0;
	let initialY = 0;
	let dragEnabled = true;

	onMount(() => {
		dragEnabled = window.matchMedia('(pointer: fine) and (hover: hover)').matches;
	});

	function handleMouseDown(e: MouseEvent) {
		if (!dragEnabled) return;
		isDragging = true;
		initialX = e.clientX - currentX;
		initialY = e.clientY - currentY;
	}

	function handleMouseMove(e: MouseEvent) {
		if (!dragEnabled || !isDragging) return;
		currentX = e.clientX - initialX;
		currentY = e.clientY - initialY;
	}

	function handleMouseUp() {
		isDragging = false;
	}
</script>

<svelte:window on:mousemove={handleMouseMove} on:mouseup={handleMouseUp} />

<div
	class="animate-in window-card w-full max-w-2xl rounded-lg border border-white/20 bg-white/10 px-6 pt-6 pb-8 text-white shadow-lg backdrop-blur-md"
	style="transform: translate({currentX}px, {currentY}px);"
>
	<div
		class="mb-8 flex items-center gap-2"
		class:cursor-move={dragEnabled}
		class:cursor-default={!dragEnabled}
		on:mousedown={handleMouseDown}
		role="toolbar"
		tabindex="0"
	>
		<div class="h-3 w-3 rounded-full bg-red-500"></div>
		<div class="h-3 w-3 rounded-full bg-yellow-500"></div>
		<div class="h-3 w-3 rounded-full bg-green-500"></div>
		{#if title}
			<span class="ml-auto text-sm font-medium opacity-70">{title}</span>
		{/if}
	</div>
	<slot />
</div>

<style>
	@keyframes windowOpen {
		0% {
			opacity: 0;
			transform: scale(0.8) translateY(-20px);
		}
		100% {
			opacity: 1;
			transform: scale(1) translateY(0);
		}
	}

	.animate-in {
		animation: windowOpen 0.4s cubic-bezier(0.16, 1, 0.3, 1);
	}

	.window-card {
		user-select: none;
	}

	@media (pointer: coarse) {
		.window-card {
			touch-action: manipulation;
		}
	}
</style>
