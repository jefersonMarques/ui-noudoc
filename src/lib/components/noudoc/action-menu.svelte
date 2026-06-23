<script lang="ts" module>
	export type ActionMenuItem = {
		label: string;
		description?: string;
		destructive?: boolean;
		disabled?: boolean;
		onSelect?: () => void;
	};
</script>

<script lang="ts">
	import EllipsisIcon from "@lucide/svelte/icons/ellipsis";
	import { Button } from "$lib/components/ui/button/index.js";
	import * as DropdownMenu from "$lib/components/ui/dropdown-menu/index.js";

	let {
		label = "Ações",
		items = [],
	}: {
		label?: string;
		items?: ActionMenuItem[];
	} = $props();
</script>

<DropdownMenu.Root>
	<DropdownMenu.Trigger>
		{#snippet child({ props })}
			<Button variant="ghost" size="icon" aria-label={label} {...props}>
				<EllipsisIcon />
			</Button>
		{/snippet}
	</DropdownMenu.Trigger>
	<DropdownMenu.Content align="end" class="min-w-44">
		<DropdownMenu.Label>{label}</DropdownMenu.Label>
		<DropdownMenu.Separator />
		{#each items as item}
			<DropdownMenu.Item
				variant={item.destructive ? "destructive" : "default"}
				disabled={item.disabled}
				onclick={item.onSelect}
			>
				<div class="grid gap-0.5">
					<span>{item.label}</span>
					{#if item.description}
						<span class="text-xs text-muted-foreground">{item.description}</span>
					{/if}
				</div>
			</DropdownMenu.Item>
		{/each}
	</DropdownMenu.Content>
</DropdownMenu.Root>
