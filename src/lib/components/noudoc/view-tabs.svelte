<script lang="ts" module>
	export type ViewTabItem = {
		id: string;
		label: string;
		href?: string;
		active?: boolean;
		disabled?: boolean;
		description?: string;
	};
</script>

<script lang="ts">
	import { cn } from "$lib/utils.js";

	let {
		items = [],
		ariaLabel = "Visualizações",
		class: className
	}: {
		items?: ViewTabItem[];
		ariaLabel?: string;
		class?: string;
	} = $props();
</script>

<nav class={cn("flex min-h-10 items-end gap-1 border-b", className)} aria-label={ariaLabel}>
	{#each items as item (item.id)}
		{#if item.href && !item.disabled}
			<a
				href={item.href}
				class={cn(
					"inline-flex h-10 items-center border-b-2 px-2.5 text-sm font-medium transition",
					item.active ? "border-foreground text-foreground" : "border-transparent text-muted-foreground hover:text-foreground"
				)}
				aria-current={item.active ? "page" : undefined}
				title={item.description}
			>
				{item.label}
			</a>
		{:else}
			<button
				type="button"
				disabled
				class="inline-flex h-10 items-center border-b-2 border-transparent px-2.5 text-sm font-medium text-muted-foreground/55"
				title={item.description ?? "Em breve"}
			>
				{item.label}
			</button>
		{/if}
	{/each}
</nav>
