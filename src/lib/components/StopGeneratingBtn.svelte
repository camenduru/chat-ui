<script lang="ts">
	import CarbonStopFilledAlt from "~icons/carbon/stop-filled-alt";

	export let classNames = "";
</script>

<button
	type="button"
	on:click
	class="btn flex h-8 rounded-lg border bg-white px-3 py-1 shadow-sm transition-all hover:bg-neutral-100 dark:border-neutral-600 dark:bg-neutral-700 dark:hover:bg-neutral-600 {classNames}"
>
	<CarbonStopFilledAlt class="-ml-1 mr-1 h-[1.25rem] w-[1.1875rem] text-neutral-300" /> Stop generating
</button>
