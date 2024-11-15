<script lang="ts">
	import CarbonRotate360 from "~icons/carbon/rotate-360";

	export let classNames = "";
</script>

<button
	type="button"
	on:click
	class="btn flex h-8 rounded-lg border bg-white px-3 py-1 text-neutral-500 shadow-sm transition-all hover:bg-neutral-100 dark:border-neutral-600 dark:bg-neutral-700 dark:text-neutral-300 dark:hover:bg-neutral-600 {classNames}"
>
	<CarbonRotate360 class="mr-2 text-xs " /> Retry
</button>
