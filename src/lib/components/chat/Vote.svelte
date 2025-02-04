<script lang="ts">
	import type { Message } from "$lib/types/Message";
	import CarbonThumbsUp from "~icons/carbon/thumbs-up";
	import CarbonThumbsDown from "~icons/carbon/thumbs-down";

	import { createEventDispatcher } from "svelte";

	export let message: Message;

	const dispatch = createEventDispatcher<{
		vote: { score: Message["score"]; id: Message["id"] };
	}>();
</script>

<button
	class="btn rounded-sm p-1 text-sm text-neutral-400 hover:text-neutral-500 focus:ring-0 dark:text-neutral-400 dark:hover:text-neutral-300
{message.score && message.score > 0
		? 'text-green-500 hover:text-green-500 dark:text-green-400 hover:dark:text-green-400'
		: ''}"
	title={message.score === 1 ? "Remove +1" : "+1"}
	type="button"
	on:click={() => dispatch("vote", { score: message.score === 1 ? 0 : 1, id: message.id })}
>
	<CarbonThumbsUp class="h-[1.14em] w-[1.14em]" />
</button>
<button
	class="btn rounded-sm p-1 text-sm text-neutral-400 hover:text-neutral-500 focus:ring-0 dark:text-neutral-400 dark:hover:text-neutral-300
{message.score && message.score < 0
		? 'text-red-500 hover:text-red-500 dark:text-red-400 hover:dark:text-red-400'
		: ''}"
	title={message.score === -1 ? "Remove -1" : "-1"}
	type="button"
	on:click={() => dispatch("vote", { score: message.score === -1 ? 0 : -1, id: message.id })}
>
	<CarbonThumbsDown class="h-[1.14em] w-[1.14em]" />
</button>
