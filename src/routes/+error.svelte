<script lang="ts">
	import { page } from "$app/stores";
</script>

<div
	class="flex items-center justify-center bg-gradient-to-t from-neutral-200 text-neutral-800 dark:from-neutral-700 dark:text-neutral-300"
>
	<div
		class="align-center -mt-24 flex flex-col justify-center rounded-xl border bg-white px-8 pb-2 pt-4 text-center dark:border-neutral-700 dark:bg-neutral-800"
	>
		<h1 class="mb-2 text-5xl font-semibold">{$page.status}</h1>
		<div class="-mx-8 my-2 h-px bg-neutral-200 dark:bg-neutral-700" />
		<h2 class="max-w-sm text-lg">{$page.error?.message}</h2>
		{#if $page.error?.errorId}
			<div class="-mx-8 my-2 h-px bg-neutral-200 dark:bg-neutral-700" />
			<pre class="max-w-sm whitespace-pre-wrap text-left font-mono text-xs">{$page.error
					.errorId}</pre>
		{/if}
	</div>
</div>
