<script lang="ts">
	import type { Snippet } from "svelte";
	import { cn } from "$lib/utils.js";

	let {
		searchLabel = "Pesquisar",
		shortcut = "Ctrl K",
		onSearch = () => {},
		onMenu = () => {},
		actions,
		class: className
	}: {
		searchLabel?: string;
		shortcut?: string;
		onSearch?: () => void;
		onMenu?: () => void;
		actions?: Snippet;
		class?: string;
	} = $props();
</script>

<header class={cn("flex h-12 items-center gap-3 border-b bg-background px-3", className)}>
	<button
		type="button"
		class="inline-flex h-8 w-8 items-center justify-center rounded-lg border bg-background text-base text-muted-foreground transition hover:bg-accent hover:text-accent-foreground lg:hidden"
		aria-label="Abrir navegação"
		onclick={onMenu}
	>
		☰
	</button>

	<button
		type="button"
		class="mx-auto hidden h-8 w-[min(520px,42vw)] items-center gap-2 rounded-lg border bg-muted/45 px-3 text-left text-sm text-muted-foreground transition hover:bg-background hover:text-foreground lg:flex"
		onclick={onSearch}
	>
		<span class="text-xs">⌕</span>
		<span class="min-w-0 flex-1 truncate">{searchLabel}</span>
		{#if shortcut}
			<kbd class="rounded border bg-background px-1.5 py-0.5 text-[10px] font-medium text-muted-foreground">{shortcut}</kbd>
		{/if}
	</button>

	<div class="ml-auto flex items-center gap-1.5">
		<button
			type="button"
			class="inline-flex h-8 w-8 items-center justify-center rounded-lg text-sm text-muted-foreground transition hover:bg-accent hover:text-accent-foreground lg:hidden"
			aria-label="Pesquisar"
			onclick={onSearch}
		>
			⌕
		</button>
		{#if actions}{@render actions()}{/if}
	</div>
</header>
