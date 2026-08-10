<script lang="ts" module>
	export type OrganizationSwitcherOption = {
		id: string;
		label: string;
	};
</script>

<script lang="ts">
	import { cn } from "$lib/utils.js";

	let {
		options = [],
		activeId = "",
		onChange = (_id: string) => {},
		class: className
	}: {
		options?: OrganizationSwitcherOption[];
		activeId?: string;
		onChange?: (id: string) => void;
		class?: string;
	} = $props();
</script>

{#if options.length > 1}
	<div class={cn("relative lg:hidden", className)}>
		<select
			data-slot="organization-switcher"
			class="h-8 w-full appearance-none rounded-lg border bg-muted/45 px-2.5 pr-7 text-xs font-medium text-foreground outline-none transition focus:border-ring focus:ring-3 focus:ring-ring/20"
			value={activeId}
			onchange={(event) => onChange(event.currentTarget.value)}
			aria-label="Trocar organização"
		>
			{#each options as option (option.id)}
				<option value={option.id}>{option.label}</option>
			{/each}
		</select>
		<span class="pointer-events-none absolute right-2.5 top-1/2 -translate-y-1/2 text-[10px] text-muted-foreground">⌄</span>
	</div>
{/if}
