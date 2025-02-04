<script lang="ts">
	export let src: string;
	export let name: string;

	import CarbonPause from "~icons/carbon/pause";
	import CarbonPlay from "~icons/carbon/play";

	let time = 0;
	let duration = 0;
	let paused = true;

	function format(time: number) {
		if (isNaN(time)) return "...";

		const minutes = Math.floor(time / 60);
		const seconds = Math.floor(time % 60);

		return `${minutes}:${seconds < 10 ? `0${seconds}` : seconds}`;
	}

	function seek(e: PointerEvent) {
		if (!e.currentTarget) return;
		const { left, width } = (e.currentTarget as HTMLElement).getBoundingClientRect();

		let p = (e.clientX - left) / width;
		if (p < 0) p = 0;
		if (p > 1) p = 1;

		time = p * duration;
	}
</script>

<div
	class="flex h-14 w-72 items-center gap-4 rounded-2xl border border-neutral-200 bg-white p-2.5 text-neutral-600 shadow-sm transition-all dark:border-neutral-800 dark:bg-neutral-800 dark:text-neutral-300"
>
	<audio
		{src}
		bind:currentTime={time}
		bind:duration
		bind:paused
		preload="metadata"
		on:ended={() => {
			time = 0;
		}}
	/>

	<button
		class="mx-auto my-auto aspect-square size-8 rounded-full border border-neutral-400 bg-neutral-100 dark:border-neutral-800 dark:bg-neutral-700"
		aria-label={paused ? "play" : "pause"}
		on:click={() => (paused = !paused)}
	>
		{#if paused}
			<CarbonPlay class="mx-auto my-auto text-neutral-600 dark:text-neutral-300" />
		{:else}
			<CarbonPause class="mx-auto my-auto text-neutral-600 dark:text-neutral-300" />
		{/if}
	</button>
	<div class="overflow-hidden">
		<div class="truncate font-medium">{name}</div>
		{#if duration !== Infinity}
			<div class="flex items-center gap-2">
				<span class="text-xs">{format(time)}</span>
				<div
					class="relative h-2 flex-1 rounded-full bg-neutral-200 dark:bg-neutral-700"
					on:pointerdown={() => {
						paused = true;
					}}
					on:pointerup={seek}
				>
					<div
						class="absolute inset-0 h-full bg-neutral-400 dark:bg-neutral-600"
						style="width: {(time / duration) * 100}%"
					/>
				</div>
				<span class="text-xs">{duration ? format(duration) : "--:--"}</span>
			</div>
		{/if}
	</div>
</div>
