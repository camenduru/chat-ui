<script lang="ts">
	import CarbonUpload from "~icons/carbon/upload";

	export let classNames = "";
	export let files: File[];
	export let mimeTypes: string[];

	/**
	 * Due to a bug with Svelte, we cannot use bind:files with multiple
	 * So we use this workaround
	 **/
	const onFileChange = (e: Event) => {
		if (!e.target) return;
		const target = e.target as HTMLInputElement;
		files = [...files, ...(target.files ?? [])];
	};
</script>

<button
	class="btn relative h-8 rounded-lg border bg-white px-3 py-1 text-sm text-neutral-500 shadow-sm hover:bg-neutral-100 dark:border-neutral-600 dark:bg-neutral-700 dark:text-neutral-300 dark:hover:bg-neutral-600 {classNames}"
>
	<input
		class="absolute w-full cursor-pointer opacity-0"
		aria-label="Upload file"
		type="file"
		on:change={onFileChange}
		accept={mimeTypes.join(",")}
	/>
	<CarbonUpload class="mr-2 text-xxs" /> Upload file
</button>
