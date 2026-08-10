<script lang="ts" module>
	export type AppSidebarItem = {
		id: string;
		label: string;
		href?: string;
		active?: boolean;
		badge?: string | number;
		disabled?: boolean;
		onSelect?: () => void;
	};
</script>

<script lang="ts">
	import type { Snippet } from "svelte";
	import { cn } from "$lib/utils.js";

	let {
		header,
		items = [],
		secondaryLabel = "Recentes",
		secondaryItems = [],
		footer,
		class: className
	}: {
		header?: Snippet;
		items?: AppSidebarItem[];
		secondaryLabel?: string;
		secondaryItems?: AppSidebarItem[];
		footer?: Snippet;
		class?: string;
	} = $props();

	function itemClass(item: AppSidebarItem) {
		return cn(
			"group flex min-h-9 w-full items-center gap-2 rounded-lg px-2.5 py-2 text-left text-sm font-medium transition",
			item.active
				? "bg-accent text-accent-foreground"
				: "text-muted-foreground hover:bg-accent/70 hover:text-accent-foreground",
			item.disabled && "cursor-not-allowed opacity-45"
		);
	}
</script>

<aside class={cn("flex h-full min-h-0 w-60 flex-col border-r bg-card", className)} aria-label="Navegação do workspace">
	{#if header}
		<div class="border-b p-3">
			{@render header()}
		</div>
	{/if}

	<nav class="min-h-0 flex-1 overflow-y-auto p-2" aria-label="Áreas">
		<div class="space-y-0.5">
			{#each items as item (item.id)}
				{#if item.href && !item.disabled}
					<a class={itemClass(item)} href={item.href} aria-current={item.active ? "page" : undefined} onclick={item.onSelect}>
						<span class="min-w-0 flex-1 truncate">{item.label}</span>
						{#if item.badge !== undefined}<span class="rounded-md bg-muted px-1.5 py-0.5 text-[10px] tabular-nums text-muted-foreground">{item.badge}</span>{/if}
					</a>
				{:else}
					<button type="button" class={itemClass(item)} disabled={item.disabled} onclick={item.onSelect}>
						<span class="min-w-0 flex-1 truncate">{item.label}</span>
						{#if item.badge !== undefined}<span class="rounded-md bg-muted px-1.5 py-0.5 text-[10px] tabular-nums text-muted-foreground">{item.badge}</span>{/if}
					</button>
				{/if}
			{/each}
		</div>

		{#if secondaryItems.length}
			<div class="mt-6">
				<p class="mb-1 px-2.5 text-[11px] font-medium text-muted-foreground">{secondaryLabel}</p>
				<div class="space-y-0.5">
					{#each secondaryItems as item (item.id)}
						{#if item.href && !item.disabled}
							<a class={itemClass(item)} href={item.href} onclick={item.onSelect}>
								<span class="min-w-0 flex-1 truncate">{item.label}</span>
							</a>
						{:else}
							<button type="button" class={itemClass(item)} disabled={item.disabled} onclick={item.onSelect}>
								<span class="min-w-0 flex-1 truncate">{item.label}</span>
							</button>
						{/if}
					{/each}
				</div>
			</div>
		{/if}
	</nav>

	{#if footer}
		<div class="border-t p-2">
			{@render footer()}
		</div>
	{/if}
</aside>
