<script lang="ts" module>
	export type AppShellNavItem = {
		label: string;
		href?: string;
		active?: boolean;
	};
</script>

<script lang="ts">
	import type { Snippet } from "svelte";
	import type { HTMLAttributes } from "svelte/elements";
	import { cn, type WithElementRef } from "$lib/utils.js";

	let {
		ref = $bindable(null),
		brand = "Noudoc",
		description = "Design System",
		navItems = [],
		rail,
		sidebar,
		header,
		children,
		mobileSidebarOpen = $bindable(false),
		class: className,
		...restProps
	}: WithElementRef<HTMLAttributes<HTMLDivElement>, HTMLDivElement> & {
		brand?: string;
		description?: string;
		navItems?: AppShellNavItem[];
		rail?: Snippet;
		sidebar?: Snippet;
		header?: Snippet;
		children?: Snippet;
		mobileSidebarOpen?: boolean;
	} = $props();

	let contextual = $derived(Boolean(rail || sidebar));
	let gridClass = $derived(
		rail && sidebar
			? "lg:grid-cols-[56px_240px_minmax(0,1fr)]"
			: rail
				? "lg:grid-cols-[56px_minmax(0,1fr)]"
				: "lg:grid-cols-[240px_minmax(0,1fr)]"
	);
</script>

<div bind:this={ref} class={cn("min-h-screen bg-background text-foreground", className)} {...restProps}>
	{#if contextual}
		<div class={cn("grid min-h-screen", gridClass)}>
			{#if rail}
				<div class="hidden min-h-screen lg:block">{@render rail()}</div>
			{/if}

			{#if sidebar}
				<div class="hidden min-h-screen lg:block">{@render sidebar()}</div>
			{/if}

			<section class="min-w-0 bg-background">
				{#if header}{@render header()}{/if}
				<main class="min-h-0 min-w-0">{@render children?.()}</main>
			</section>
		</div>

		{#if sidebar && mobileSidebarOpen}
			<div class="fixed inset-0 z-50 lg:hidden">
				<button
					type="button"
					class="absolute inset-0 h-full w-full bg-foreground/25"
					aria-label="Fechar navegação"
					onclick={() => (mobileSidebarOpen = false)}
				></button>
				<div class="relative h-full w-72 max-w-[88vw] bg-card shadow-xl">{@render sidebar()}</div>
			</div>
		{/if}
	{:else}
		<div class="grid min-h-screen lg:grid-cols-[260px_minmax(0,1fr)]">
			<aside class="border-r bg-card/60 p-4">
				<div class="mb-6 rounded-lg border bg-background p-3 shadow-xs">
					<p class="text-sm font-medium">{brand}</p>
					<p class="text-xs text-muted-foreground">{description}</p>
				</div>

				<nav class="grid gap-1">
					{#each navItems as item}
						{#if item.href}
							<a
								href={item.href}
								class={cn(
									"rounded-md px-3 py-2 text-left text-sm transition hover:bg-accent hover:text-accent-foreground",
									item.active ? "bg-accent font-medium text-accent-foreground" : "text-muted-foreground"
								)}
							>
								{item.label}
							</a>
						{:else}
							<button
								type="button"
								class={cn(
									"rounded-md px-3 py-2 text-left text-sm transition hover:bg-accent hover:text-accent-foreground",
									item.active ? "bg-accent font-medium text-accent-foreground" : "text-muted-foreground"
								)}
							>
								{item.label}
							</button>
						{/if}
					{/each}
				</nav>
			</aside>

			<section class="min-w-0">
				{#if header}
					<div class="border-b bg-background/80 p-4 backdrop-blur supports-[backdrop-filter]:bg-background/60">
						{@render header()}
					</div>
				{/if}

				<main class="p-4 sm:p-6">{@render children?.()}</main>
			</section>
		</div>
	{/if}
</div>
