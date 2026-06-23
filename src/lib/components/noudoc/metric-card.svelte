<script lang="ts">
	import type { Snippet } from "svelte";
	import type { HTMLAttributes } from "svelte/elements";
	import * as Card from "$lib/components/ui/card/index.js";
	import { Badge } from "$lib/components/ui/badge/index.js";
	import { cn, type WithElementRef } from "$lib/utils.js";

	type TrendVariant = "neutral" | "positive" | "negative" | "warning";

	let {
		ref = $bindable(null),
		label,
		value,
		description,
		trend,
		trendVariant = "neutral",
		children,
		class: className,
		...restProps
	}: WithElementRef<HTMLAttributes<HTMLDivElement>, HTMLDivElement> & {
		label: string;
		value: string | number;
		description?: string;
		trend?: string;
		trendVariant?: TrendVariant;
		children?: Snippet;
	} = $props();

	const trendClass: Record<TrendVariant, string> = {
		neutral: "",
		positive: "border-emerald-200 bg-emerald-50 text-emerald-700 dark:border-emerald-900 dark:bg-emerald-950 dark:text-emerald-300",
		negative: "border-destructive/20 bg-destructive/10 text-destructive dark:bg-destructive/20",
		warning: "border-amber-200 bg-amber-50 text-amber-700 dark:border-amber-900 dark:bg-amber-950 dark:text-amber-300",
	};
</script>

<Card.Root bind:ref class={cn("min-w-0", className)} {...restProps}>
	<Card.Header class="flex flex-row items-start justify-between gap-3">
		<div class="min-w-0">
			<Card.Description>{label}</Card.Description>
			<Card.Title class="mt-2 text-2xl font-semibold tracking-tight">{value}</Card.Title>
		</div>
		{#if trend}
			<Badge variant="outline" class={trendClass[trendVariant]}>{trend}</Badge>
		{/if}
	</Card.Header>

	{#if description || children}
		<Card.Content class="space-y-3">
			{#if description}
				<p class="text-sm text-muted-foreground">{description}</p>
			{/if}
			{#if children}
				{@render children()}
			{/if}
		</Card.Content>
	{/if}
</Card.Root>
