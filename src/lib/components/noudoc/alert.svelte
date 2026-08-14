<script lang="ts">
	import AlertCircle from '@lucide/svelte/icons/circle-alert';
	import AlertTriangle from '@lucide/svelte/icons/triangle-alert';
	import CheckCircle2 from '@lucide/svelte/icons/circle-check-big';
	import Info from '@lucide/svelte/icons/info';
	import type { Snippet } from 'svelte';
	import type { HTMLAttributes } from 'svelte/elements';
	import { cn, type WithElementRef } from '$lib/utils.js';

	export type AlertTone = 'info' | 'success' | 'warning' | 'danger';

	let {
		ref = $bindable(null),
		tone = 'info',
		title,
		description,
		children,
		class: className,
		...restProps
	}: WithElementRef<HTMLAttributes<HTMLDivElement>, HTMLDivElement> & {
		tone?: AlertTone;
		title?: string;
		description?: string;
		children?: Snippet;
	} = $props();

	const toneClasses: Record<AlertTone, string> = {
		info: 'border-sky-200/70 bg-sky-50/70 text-sky-800 dark:border-sky-900 dark:bg-sky-950/40 dark:text-sky-300',
		success: 'border-emerald-200/70 bg-emerald-50/70 text-emerald-800 dark:border-emerald-900 dark:bg-emerald-950/40 dark:text-emerald-300',
		warning: 'border-amber-200/70 bg-amber-50/70 text-amber-800 dark:border-amber-900 dark:bg-amber-950/40 dark:text-amber-300',
		danger: 'border-destructive/20 bg-destructive/10 text-destructive dark:bg-destructive/20'
	};

	const icons = {
		info: Info,
		success: CheckCircle2,
		warning: AlertTriangle,
		danger: AlertCircle
	};

	let Icon = $derived(icons[tone]);
</script>

<div
	bind:this={ref}
	data-slot="noudoc-alert"
	role={tone === 'danger' ? 'alert' : 'status'}
	class={cn('rounded-2xl border p-4', toneClasses[tone], className)}
	{...restProps}
>
	<div class="flex gap-3">
		<div class="mt-0.5 flex size-8 shrink-0 items-center justify-center rounded-xl bg-background/70">
			<Icon class="size-4" />
		</div>
		<div class="min-w-0 flex-1">
			{#if title}
				<p class="text-sm font-semibold">{title}</p>
			{/if}
			{#if description}
				<p class={cn('text-sm leading-6 opacity-80', title && 'mt-1')}>{description}</p>
			{/if}
			{@render children?.()}
		</div>
	</div>
</div>
