<script lang="ts">
	import type { Snippet } from "svelte";
	import type { HTMLAttributes } from "svelte/elements";
	import { cn, type WithElementRef } from "$lib/utils.js";

	let {
		ref = $bindable(null),
		title,
		description,
		children,
		class: className,
		...restProps
	}: WithElementRef<HTMLAttributes<HTMLElement>, HTMLElement> & {
		title: string;
		description?: string;
		children?: Snippet;
	} = $props();
</script>

<div
	bind:this={ref}
	class={cn("flex flex-col gap-3 sm:flex-row sm:items-center sm:justify-between", className)}
	{...restProps}
>
	<div class="min-w-0">
		<h2 class="text-base font-medium text-foreground">{title}</h2>
		{#if description}
			<p class="mt-1 text-sm text-muted-foreground">{description}</p>
		{/if}
	</div>

	{#if children}
		<div class="flex shrink-0 flex-wrap items-center gap-2">
			{@render children()}
		</div>
	{/if}
</div>
