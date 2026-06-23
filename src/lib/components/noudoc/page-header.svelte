<script lang="ts">
	import type { Snippet } from "svelte";
	import type { HTMLAttributes } from "svelte/elements";
	import { cn, type WithElementRef } from "$lib/utils.js";

	let {
		ref = $bindable(null),
		eyebrow,
		title,
		description,
		children,
		class: className,
		...restProps
	}: WithElementRef<HTMLAttributes<HTMLElement>, HTMLElement> & {
		eyebrow?: string;
		title: string;
		description?: string;
		children?: Snippet;
	} = $props();
</script>

<header
	bind:this={ref}
	class={cn("flex flex-col gap-4 border-b pb-6 sm:flex-row sm:items-end sm:justify-between", className)}
	{...restProps}
>
	<div class="min-w-0">
		{#if eyebrow}
			<p class="text-xs font-medium uppercase tracking-wide text-muted-foreground">{eyebrow}</p>
		{/if}
		<h1 class="mt-1 text-3xl font-semibold tracking-tight text-foreground">{title}</h1>
		{#if description}
			<p class="mt-2 max-w-2xl text-sm text-muted-foreground">{description}</p>
		{/if}
	</div>

	{#if children}
		<div class="flex shrink-0 flex-wrap items-center gap-2">
			{@render children()}
		</div>
	{/if}
</header>
