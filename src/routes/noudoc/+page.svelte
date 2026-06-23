<script lang="ts">
	import { Button } from "$lib/components/ui/button/index.js";
	import MetricCard from "$lib/components/noudoc/metric-card.svelte";
	import PageHeader from "$lib/components/noudoc/page-header.svelte";
</script>

<main class="mx-auto min-h-screen max-w-7xl space-y-8 px-5 py-6">
	<PageHeader
		eyebrow="Noudoc"
		title="Componentes próprios"
		description="Camada de produto construída sobre os componentes oficiais."
	>
		<Button href="/components" variant="outline">Componentes oficiais</Button>
		<Button>Novo workspace</Button>
	</PageHeader>

	<section class="grid gap-4 md:grid-cols-3">
		<MetricCard label="Workspaces ativos" value="18" trend="+12%" trendVariant="positive" description="Crescimento nos últimos 30 dias." />
		<MetricCard label="Tarefas pendentes" value="42" trend="8" trendVariant="warning" description="Itens aguardando revisão." />
		<MetricCard label="Automações" value="96%" trend="OK" description="Execuções concluídas sem erro." />
	</section>
</main>
