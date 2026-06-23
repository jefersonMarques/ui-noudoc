# @noudoc/ui

Biblioteca de UI da Noudoc baseada em componentes oficiais do `shadcn-svelte`.

## Regra principal

Não editar componentes base manualmente.

Componentes oficiais ficam em:

```txt
src/lib/components/ui
```

Componentes próprios da Noudoc ficam separados em:

```txt
src/lib/components/noudoc
```

## Rodar localmente

```bash
npm install
npm run check
npm run build
npm run dev
```

Rotas úteis:

```txt
/components  componentes oficiais
/noudoc      componentes próprios Noudoc
```

## Componentes oficiais instalados

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

O `sidebar` também instala dependências oficiais como `sheet`, `skeleton` e `is-mobile`.

## Atualizar componentes oficiais

Use sempre a CLI do shadcn-svelte:

```bash
npm run ui:add:base
```

Evite alterar manualmente arquivos em `src/lib/components/ui`, porque isso quebra a compatibilidade com o padrão do shadcn.

## Componentes Noudoc

Primeiros componentes próprios criados:

```txt
src/lib/components/noudoc/action-menu.svelte
src/lib/components/noudoc/app-shell.svelte
src/lib/components/noudoc/data-toolbar.svelte
src/lib/components/noudoc/metric-card.svelte
src/lib/components/noudoc/page-header.svelte
src/lib/components/noudoc/section-header.svelte
src/lib/components/noudoc/status-badge.svelte
```

Esses componentes podem compor os oficiais, mas não devem substituir os componentes base do shadcn.

## Importação

```ts
import { Button, Card, PageHeader, MetricCard, StatusBadge } from "@noudoc/ui";
```
