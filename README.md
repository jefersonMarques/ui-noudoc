# @noudoc/ui

Projeto limpo para padronizar os projetos Noudoc usando componentes oficiais do `shadcn-svelte`.

## Regra principal

Não editar componentes base manualmente.

Componentes oficiais ficam em:

```txt
src/lib/components/ui
```

Componentes próprios da Noudoc devem ficar separados em:

```txt
src/lib/components/noudoc
```

## Setup limpo

O projeto já foi criado com SvelteKit Library + Tailwind CSS.

Rode localmente:

```bash
npm install
npm run ui:init
npm run ui:add:base
npm run check
npm run dev
```

## Componentes oficiais adicionados pelo comando

```txt
button
field
input
textarea
select
checkbox
switch
badge
card
dialog
dropdown-menu
popover
tooltip
table
tabs
empty
sidebar
```

## Subir no GitHub

Crie o repositório vazio no GitHub com o nome `noudoc-ui` e rode:

```bash
git init
git add .
git commit -m "Initial clean shadcn-svelte setup"
git branch -M main
git remote add origin https://github.com/jefersonMarques/noudoc-ui.git
git push -u origin main
```

## Depois do shadcn oficial

Só depois de rodar `npm run ui:add:base`, crie os componentes próprios de produto:

```txt
src/lib/components/noudoc/app-shell.svelte
src/lib/components/noudoc/page-header.svelte
src/lib/components/noudoc/data-toolbar.svelte
src/lib/components/noudoc/metric-card.svelte
src/lib/components/noudoc/status-badge.svelte
```

Esses componentes podem compor os oficiais, mas não devem substituir os componentes base do shadcn.
