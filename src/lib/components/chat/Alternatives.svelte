<script lang="ts">
	import type { Message } from "$lib/types/Message";
	import CarbonTrashCan from "~icons/carbon/trash-can";
	import CarbonChevronLeft from "~icons/carbon/chevron-left";
	import CarbonChevronRight from "~icons/carbon/chevron-right";

	import { enhance } from "$app/forms";

	export let message: Message;
	export let childToRender: number;
	export let nChildren: number;
	export let loading = false;
</script>

<div
	class="font-white group/navbranch z-0 -mt-1 ml-3.5 mr-auto flex h-6 w-fit select-none flex-row items-center justify-center gap-1 text-sm"
>
	<button
		class="inline text-lg font-thin text-neutral-400 hover:text-neutral-800 disabled:pointer-events-none disabled:opacity-25 dark:text-neutral-500 dark:hover:text-neutral-200"
		on:click={() => (childToRender = Math.max(0, childToRender - 1))}
		disabled={childToRender === 0 || loading}
	>
		<CarbonChevronLeft class="text-sm" />
	</button>
	<span class=" text-neutral-400 dark:text-neutral-500">
		{childToRender + 1} / {nChildren}
	</span>
	<button
		class="inline text-lg font-thin text-neutral-400 hover:text-neutral-800 disabled:pointer-events-none disabled:opacity-25 dark:text-neutral-500 dark:hover:text-neutral-200"
		on:click={() =>
			(childToRender = Math.min(message?.children?.length ?? 1 - 1, childToRender + 1))}
		disabled={childToRender === nChildren - 1 || loading}
	>
		<CarbonChevronRight class="text-sm" />
	</button>
	{#if !loading && message.children}<form
			method="POST"
			action="?/deleteBranch"
			class="hidden group-hover/navbranch:block"
			use:enhance={({ cancel }) => {
				if (!confirm("Are you sure you want to delete this branch?")) {
					cancel();
				}
			}}
		>
			<input name="messageId" value={message.children[childToRender]} type="hidden" />
			<button
				class="flex items-center justify-center text-xs text-neutral-400 hover:text-neutral-800 dark:text-neutral-500 dark:hover:text-neutral-200"
				type="submit"
				><CarbonTrashCan />
			</button>
		</form>
	{/if}
</div>
