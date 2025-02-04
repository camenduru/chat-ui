<script lang="ts">
	import Modal from "./Modal.svelte";
	import CarbonClose from "~icons/carbon/close";
	import CarbonBlockchain from "~icons/carbon/blockchain";

	export let preprompt: string;

	let isOpen = false;
</script>

<button
	type="button"
	class="mx-auto flex items-center gap-1.5 rounded-full border border-neutral-100 bg-neutral-50 px-3 py-1 text-xs text-neutral-500 hover:bg-neutral-100 dark:border-neutral-800 dark:bg-neutral-800 dark:text-neutral-400 dark:hover:bg-neutral-700"
	on:click={() => (isOpen = !isOpen)}
	on:keydown={(e) => e.key === "Enter" && (isOpen = !isOpen)}
>
	<CarbonBlockchain class="text-xxs" /> Using Custom System Prompt
</button>

{#if isOpen}
	<Modal on:close={() => (isOpen = false)} width="w-full max-w-2xl">
		<div class="flex w-full flex-col gap-5 p-6">
			<div class="flex items-start justify-between text-xl font-semibold text-neutral-800">
				<h2>System Prompt</h2>
				<button type="button" class="group" on:click={() => (isOpen = false)}>
					<CarbonClose class="mt-auto text-neutral-800 group-hover:text-neutral-500" />
				</button>
			</div>
			<textarea
				disabled
				value={preprompt}
				class="min-h-[420px] w-full resize-none rounded-lg border bg-neutral-50 p-2.5 text-neutral-600 max-sm:text-sm"
			/>
		</div>
	</Modal>
{/if}
