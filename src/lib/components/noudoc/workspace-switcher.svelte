<script lang="ts" module>
	export type WorkspaceSwitcherOption = {
		id: string;
		label: string;
		description?: string;
	};
</script>

<script lang="ts">
	import { cn } from "$lib/utils.js";

	let {
		organizationLabel,
		options = [],
		activeId = "",
		emptyLabel = "Nenhum workspace",
		onChange = (_id: string) => {},
		class: className
	}: {
		organizationLabel?: string;
		options?: WorkspaceSwitcherOption[];
		activeId?: string;
		emptyLabel?: string;
		onChange?: (id: string) => void;
		class?: string;
	} = $props();

	let selectedId = $derived(activeId || options[0]?.id || "");
	let selected = $derived(options.find((item) => item.id === selectedId) ?? null);
</script>

<div class={cn("min-w-0", className)}>
	{#if organizationLabel}
		<p class="mb-1 truncate px-1 text-[11px] font-medium text-muted-foreground">{organizationLabel}</p>
	{/if}

	{#if options.length > 1}
		<div class="relative">
			<select
				data-slot="workspace-switcher"
				class="h-9 w-full appearance-none rounded-lg border bg-background px-3 pr-8 text-sm font-medium text-foreground shadow-xs outline-none transition focus:border-ring focus:ring-3 focus:ring-ring/20"
				value={selectedId}
				onchange={(event) => onChange(event.currentTarget.value)}
				aria-label="Trocar workspace"
			>
				{#each options as option (option.id)}
					<option value={option.id}>{option.label}</option>
				{/each}
			</select>
			<span class="pointer-events-none absolute right-3 top-1/2 -translate-y-1/2 text-xs text-muted-foreground">⌄</span>
		</div>
	{:else}
		<div class="rounded-lg border bg-background px-3 py-2 shadow-xs">
			<p class="truncate text-sm font-medium text-foreground">{selected?.label ?? emptyLabel}</p>
			{#if selected?.description}
				<p class="mt-0.5 truncate text-xs text-muted-foreground">{selected.description}</p>
			{/if}
		</div>
	{/if}
</div>
