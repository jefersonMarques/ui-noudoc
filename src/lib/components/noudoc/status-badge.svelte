<script lang="ts">
	import type { Snippet } from "svelte";
	import type { HTMLAnchorAttributes } from "svelte/elements";
	import { Badge } from "$lib/components/ui/badge/index.js";
	import { cn, type WithElementRef } from "$lib/utils.js";

	type Status = "success" | "warning" | "danger" | "info" | "neutral" | "draft";

	let {
		ref = $bindable(null),
		status = "neutral",
		children,
		class: className,
		...restProps
	}: WithElementRef<HTMLAnchorAttributes, HTMLElement> & {
		status?: Status;
		children?: Snippet;
	} = $props();

	const statusClass: Record<Status, string> = {
		success: "border-emerald-200 bg-emerald-50 text-emerald-700 dark:border-emerald-900 dark:bg-emerald-950 dark:text-emerald-300",
		warning: "border-amber-200 bg-amber-50 text-amber-700 dark:border-amber-900 dark:bg-amber-950 dark:text-amber-300",
		danger: "border-destructive/20 bg-destructive/10 text-destructive dark:bg-destructive/20",
		info: "border-sky-200 bg-sky-50 text-sky-700 dark:border-sky-900 dark:bg-sky-950 dark:text-sky-300",
		neutral: "border-border bg-muted text-muted-foreground",
		draft: "border-border bg-background text-muted-foreground",
	};
</script>

<Badge bind:ref variant="outline" class={cn("gap-1.5", statusClass[status], className)} {...restProps}>
	<span class="size-1.5 rounded-full bg-current opacity-70"></span>
	{@render children?.()}
</Badge>
