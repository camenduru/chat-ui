<script lang="ts">
	export let isCollapsed: boolean;
	export let classNames: string;
</script>

<button
	on:click
	class="{classNames} group flex h-16 w-6 flex-col items-center justify-center -space-y-1 outline-none *:h-3 *:w-1 *:rounded-full *:hover:bg-neutral-300 dark:*:hover:bg-neutral-600 max-md:hidden {!isCollapsed
		? '*:bg-neutral-200/70 dark:*:bg-neutral-800'
		: '*:bg-neutral-200 dark:*:bg-neutral-700'}"
	name="sidebar-toggle"
	aria-label="Toggle sidebar navigation"
>
	<div class={!isCollapsed ? "group-hover:rotate-[20deg]" : "group-hover:-rotate-[20deg]"} />
	<div class={!isCollapsed ? "group-hover:-rotate-[20deg]" : "group-hover:rotate-[20deg]"} />
</button>
