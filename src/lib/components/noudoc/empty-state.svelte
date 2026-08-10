<script lang="ts">
	import type { Snippet } from "svelte";
	import { cn } from "$lib/utils.js";

	let {
		title = "Nada encontrado",
		description = "",
		actions,
		class: className
	}: {
		title?: string;
		description?: string;
		actions?: Snippet;
		class?: string;
	} = $props();
</script>

<div class={cn("rounded-xl border border-dashed bg-card px-6 py-8 text-center text-card-foreground", className)} data-slot="empty-state">
	<h3 class="text-sm font-semibold text-foreground">{title}</h3>
	{#if description}
		<p class="mx-auto mt-1 max-w-lg text-sm leading-6 text-muted-foreground">{description}</p>
	{/if}
	{#if actions}
		<div class="mt-4 flex flex-wrap items-center justify-center gap-2">{@render actions()}</div>
	{/if}
</div>
