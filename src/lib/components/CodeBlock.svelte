<script lang="ts">
	import { afterUpdate } from "svelte";
	import CopyToClipBoardBtn from "./CopyToClipBoardBtn.svelte";
	import DOMPurify from "isomorphic-dompurify";

	export let code = "";
	export let lang = "";

	$: highlightedCode = "";

	afterUpdate(async () => {
		const { default: hljs } = await import("highlight.js");
		const language = hljs.getLanguage(lang);

		highlightedCode = hljs.highlightAuto(code, language?.aliases).value;
	});
</script>

<div class="group relative my-4 rounded-lg">
	<!-- eslint-disable svelte/no-at-html-tags -->
	<pre
		class="scrollbar-custom overflow-auto px-5 scrollbar-thumb-neutral-500 hover:scrollbar-thumb-neutral-400 dark:scrollbar-thumb-white/10 dark:hover:scrollbar-thumb-white/20"><code
			class="language-{lang}"
			>{@html DOMPurify.sanitize(highlightedCode || code.replaceAll("<", "&lt;"))}
		</code></pre>
	<CopyToClipBoardBtn
		classNames="btn rounded-lg border border-neutral-200 px-2 py-2 text-sm shadow-sm transition-all hover:border-neutral-300 active:shadow-inner dark:border-neutral-700 dark:hover:border-neutral-500 absolute top-2 right-2 invisible opacity-0 group-hover:visible group-hover:opacity-100 dark:text-neutral-700 text-neutral-200"
		value={code}
	/>
</div>
