<script lang="ts">
	import type { Snippet } from 'svelte';
	import type { HTMLAttributes } from 'svelte/elements';
	import { cn, type WithElementRef } from '$lib/utils.js';

	let {
		ref = $bindable(null),
		title = 'Carregando...',
		description,
		children,
		class: className,
		...restProps
	}: WithElementRef<HTMLAttributes<HTMLDivElement>, HTMLDivElement> & {
		title?: string;
		description?: string;
		children?: Snippet;
	} = $props();
</script>

<div
	bind:this={ref}
	data-slot="noudoc-loading-state"
	class={cn('flex min-h-40 flex-col items-center justify-center rounded-2xl border bg-card p-8 text-center shadow-xs', className)}
	role="status"
	aria-live="polite"
	{...restProps}
>
	<div class="size-7 animate-spin rounded-full border-2 border-border border-t-foreground" aria-hidden="true"></div>
	<p class="mt-4 text-sm font-semibold text-foreground">{title}</p>
	{#if description}
		<p class="mt-1 max-w-md text-sm leading-6 text-muted-foreground">{description}</p>
	{/if}
	{@render children?.()}
</div>
