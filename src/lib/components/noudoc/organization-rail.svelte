<script lang="ts" module>
	export type OrganizationRailItem = {
		id: string;
		label: string;
		shortLabel?: string;
		active?: boolean;
	};
</script>

<script lang="ts">
	import { cn } from "$lib/utils.js";

	let {
		items = [],
		homeLabel = "Minha central",
		homeActive = false,
		onHomeSelect = () => {},
		onSelect = (_id: string) => {},
		onAdd = () => {},
		class: className
	}: {
		items?: OrganizationRailItem[];
		homeLabel?: string;
		homeActive?: boolean;
		onHomeSelect?: () => void;
		onSelect?: (id: string) => void;
		onAdd?: () => void;
		class?: string;
	} = $props();

	function initials(item: OrganizationRailItem) {
		if (item.shortLabel?.trim()) return item.shortLabel.trim().slice(0, 3).toUpperCase();
		return item.label
			.split(/\s+/)
			.filter(Boolean)
			.slice(0, 2)
			.map((part) => part.slice(0, 1))
			.join("")
			.toUpperCase() || "ORG";
	}
</script>

<aside class={cn("flex h-full w-14 flex-col items-center border-r border-white/10 bg-foreground px-2 py-2 text-background", className)} aria-label="Organizações">
	<button
		type="button"
		class={cn(
			"flex h-9 w-9 items-center justify-center rounded-lg text-xs font-semibold transition",
			homeActive ? "bg-background text-foreground" : "bg-background/10 text-background hover:bg-background/15"
		)}
		title={homeLabel}
		aria-label={homeLabel}
		onclick={onHomeSelect}
	>
		N
	</button>

	<div class="my-2 h-px w-7 bg-background/15"></div>

	<nav class="flex min-h-0 flex-1 flex-col items-center gap-1 overflow-y-auto" aria-label="Trocar organização">
		{#each items as item (item.id)}
			<button
				type="button"
				class={cn(
					"relative flex h-9 w-9 shrink-0 items-center justify-center rounded-lg text-[10px] font-semibold transition",
					item.active ? "bg-background text-foreground" : "bg-background/8 text-background/75 hover:bg-background/15 hover:text-background"
				)}
				title={item.label}
				aria-label={`Abrir ${item.label}`}
				onclick={() => onSelect(item.id)}
			>
				{initials(item)}
				{#if item.active}
					<span class="absolute -left-2 h-5 w-0.5 rounded-r-full bg-background"></span>
				{/if}
			</button>
		{/each}
	</nav>

	<button
		type="button"
		class="mt-2 flex h-9 w-9 items-center justify-center rounded-lg border border-background/15 text-lg font-light text-background/70 transition hover:bg-background/10 hover:text-background"
		title="Nova organização"
		aria-label="Nova organização"
		onclick={onAdd}
	>
		+
	</button>
</aside>
