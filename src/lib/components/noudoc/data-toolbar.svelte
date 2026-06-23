<script lang="ts">
	import type { Snippet } from "svelte";
	import type { HTMLAttributes } from "svelte/elements";
	import { Input } from "$lib/components/ui/input/index.js";
	import { cn, type WithElementRef } from "$lib/utils.js";

	let {
		ref = $bindable(null),
		search = $bindable(""),
		searchPlaceholder = "Buscar...",
		filters,
		actions,
		class: className,
		...restProps
	}: WithElementRef<HTMLAttributes<HTMLDivElement>, HTMLDivElement> & {
		search?: string;
		searchPlaceholder?: string;
		filters?: Snippet;
		actions?: Snippet;
	} = $props();
</script>

<div
	bind:this={ref}
	class={cn("flex flex-col gap-3 rounded-xl border bg-card p-3 shadow-xs sm:flex-row sm:items-center sm:justify-between", className)}
	{...restProps}
>
	<div class="flex min-w-0 flex-1 flex-col gap-2 sm:flex-row sm:items-center">
		<Input bind:value={search} class="sm:max-w-xs" placeholder={searchPlaceholder} />
		{#if filters}
			<div class="flex flex-wrap items-center gap-2">
				{@render filters()}
			</div>
		{/if}
	</div>

	{#if actions}
		<div class="flex shrink-0 flex-wrap items-center gap-2">
			{@render actions()}
		</div>
	{/if}
</div>
