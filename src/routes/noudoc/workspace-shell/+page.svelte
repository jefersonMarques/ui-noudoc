<script lang="ts">
	import AppHeader from "$lib/components/noudoc/app-header.svelte";
	import AppShell from "$lib/components/noudoc/app-shell.svelte";
	import AppSidebar from "$lib/components/noudoc/app-sidebar.svelte";
	import OrganizationRail from "$lib/components/noudoc/organization-rail.svelte";
	import OrganizationSwitcher from "$lib/components/noudoc/organization-switcher.svelte";
	import WorkspaceSwitcher from "$lib/components/noudoc/workspace-switcher.svelte";
	import { Badge } from "$lib/components/ui/badge/index.js";

	let organizationId = "f10";
	let workspaceId = "blog";
	let mobileSidebarOpen = false;

	const organizations = [
		{ id: "f10", label: "F10 Software" },
		{ id: "viagate", label: "Viagate" },
		{ id: "noudoc", label: "Noudoc" }
	];

	const workspaces = [
		{ id: "blog", label: "Blog F10", description: "f10.com.br" },
		{ id: "academy", label: "Academy", description: "Conteúdo educacional" }
	];

	$: railItems = organizations.map((item) => ({ ...item, active: item.id === organizationId }));
	$: sidebarItems = [
		{ id: "nia", label: "NIA" },
		{ id: "my-work", label: "Meu trabalho", href: "#", active: true },
		{ id: "production", label: "Produção", href: "#" },
		{ id: "knowledge", label: "Conhecimento", href: "#" },
		{ id: "settings", label: "Configurações" }
	];
</script>

<div class="h-screen overflow-hidden">
	<AppShell bind:mobileSidebarOpen showRail={organizations.length > 1}>
		{#snippet rail()}
			<OrganizationRail
				items={railItems}
				onSelect={(id) => (organizationId = id)}
				onAdd={() => {}}
			/>
		{/snippet}

		{#snippet sidebar()}
			<AppSidebar items={sidebarItems} secondaryLabel="Recentes" secondaryItems={[{ id: "recent-1", label: "Funil de matrículas", href: "#" }]}>
				{#snippet header()}
					<div class="space-y-2">
						<div>
							<p class="text-sm font-semibold">Noudoc</p>
							<p class="text-xs text-muted-foreground">AI workspace</p>
						</div>
						<OrganizationSwitcher options={organizations} activeId={organizationId} onChange={(id) => (organizationId = id)} />
						<WorkspaceSwitcher organizationLabel={organizations.find((item) => item.id === organizationId)?.label} options={workspaces} activeId={workspaceId} onChange={(id) => (workspaceId = id)} />
					</div>
				{/snippet}
			</AppSidebar>
		{/snippet}

		{#snippet header()}
			<AppHeader onMenu={() => (mobileSidebarOpen = true)} onSearch={() => {}}>
				{#snippet actions()}<Badge variant="secondary">NIA ativa</Badge>{/snippet}
			</AppHeader>
		{/snippet}

		<div class="p-5 sm:p-7">
			<div class="mx-auto max-w-5xl">
				<p class="text-sm text-muted-foreground">Meu trabalho</p>
				<div class="mt-2 flex items-end justify-between gap-4 border-b pb-4">
					<div>
						<h1 class="text-2xl font-semibold tracking-tight">Lista</h1>
						<p class="mt-1 text-sm text-muted-foreground">Exemplo do shell adaptativo multi-entidade.</p>
					</div>
				</div>
				<div class="mt-4 divide-y rounded-lg border bg-card">
					{#each ["Definir CTA principal", "Mapear conteúdo do site", "Criar plano editorial"] as task, index}
						<div class="grid grid-cols-[1fr_160px_140px] gap-3 px-4 py-3 text-sm">
							<span>{task}</span>
							<span class="text-muted-foreground">{index === 0 ? "Jeferson" : "NIA"}</span>
							<span class="text-muted-foreground">{index === 0 ? "Precisa de você" : "Executando"}</span>
						</div>
					{/each}
				</div>
			</div>
		</div>
	</AppShell>
</div>
