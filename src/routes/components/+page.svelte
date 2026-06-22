<script lang="ts">
  import { Button } from '$lib/components/ui/button/index.js';
  import { Input } from '$lib/components/ui/input/index.js';
  import { Textarea } from '$lib/components/ui/textarea/index.js';
  import { Checkbox } from '$lib/components/ui/checkbox/index.js';
  import { Switch } from '$lib/components/ui/switch/index.js';
  import { Badge } from '$lib/components/ui/badge/index.js';
  import * as Card from '$lib/components/ui/card/index.js';
  import * as Field from '$lib/components/ui/field/index.js';
  import * as Dialog from '$lib/components/ui/dialog/index.js';
  import * as DropdownMenu from '$lib/components/ui/dropdown-menu/index.js';
  import * as Popover from '$lib/components/ui/popover/index.js';
  import * as Tooltip from '$lib/components/ui/tooltip/index.js';
  import * as Select from '$lib/components/ui/select/index.js';
  import * as Table from '$lib/components/ui/table/index.js';
  import * as Tabs from '$lib/components/ui/tabs/index.js';
  import * as Empty from '$lib/components/ui/empty/index.js';
  import * as Sidebar from '$lib/components/ui/sidebar/index.js';

  type ComponentDoc = {
    slug: string;
    name: string;
    category: string;
    description: string;
    code: string;
  };

  const componentDocs: ComponentDoc[] = [
    {
      slug: 'button',
      name: 'Button',
      category: 'Core',
      description: 'Botão base com variantes oficiais do shadcn-svelte.',
      code: 'import { Button } from "$lib/components/ui/button/index.js";\n\n<Button>Save</Button>\n<Button variant="outline">Cancel</Button>'
    },
    {
      slug: 'input',
      name: 'Input',
      category: 'Form',
      description: 'Campo de texto padrão para formulários.',
      code: 'import { Input } from "$lib/components/ui/input/index.js";\n\n<Input type="email" placeholder="admin@noudoc.com" />'
    },
    {
      slug: 'textarea',
      name: 'Textarea',
      category: 'Form',
      description: 'Campo multilinha para observações e textos maiores.',
      code: 'import { Textarea } from "$lib/components/ui/textarea/index.js";\n\n<Textarea placeholder="Digite uma observação" />'
    },
    {
      slug: 'field',
      name: 'Field',
      category: 'Form',
      description: 'Composição para label, descrição, erro e controle.',
      code: 'import * as Field from "$lib/components/ui/field/index.js";\nimport { Input } from "$lib/components/ui/input/index.js";\n\n<Field.Root>\n  <Field.Label>Nome</Field.Label>\n  <Input placeholder="Nome do workspace" />\n  <Field.Description>Nome visível no sistema.</Field.Description>\n</Field.Root>'
    },
    {
      slug: 'checkbox',
      name: 'Checkbox',
      category: 'Form',
      description: 'Controle booleano com estado marcado/desmarcado.',
      code: 'import { Checkbox } from "$lib/components/ui/checkbox/index.js";\n\n<Checkbox bind:checked />'
    },
    {
      slug: 'switch',
      name: 'Switch',
      category: 'Form',
      description: 'Alternância rápida para recursos ligados/desligados.',
      code: 'import { Switch } from "$lib/components/ui/switch/index.js";\n\n<Switch bind:checked />'
    },
    {
      slug: 'select',
      name: 'Select',
      category: 'Form',
      description: 'Seleção de uma opção usando primitive oficial.',
      code: 'import * as Select from "$lib/components/ui/select/index.js";\n\n<Select.Root type="single" bind:value={value}>\n  <Select.Trigger>{selectedLabel}</Select.Trigger>\n  <Select.Content>\n    <Select.Item value="admin">Admin</Select.Item>\n  </Select.Content>\n</Select.Root>'
    },
    {
      slug: 'badge',
      name: 'Badge',
      category: 'Core',
      description: 'Rótulos curtos para status, categorias e estados.',
      code: 'import { Badge } from "$lib/components/ui/badge/index.js";\n\n<Badge>Default</Badge>\n<Badge variant="secondary">Draft</Badge>'
    },
    {
      slug: 'card',
      name: 'Card',
      category: 'Layout',
      description: 'Container para agrupar conteúdo, ações e descrições.',
      code: 'import * as Card from "$lib/components/ui/card/index.js";\n\n<Card.Root>\n  <Card.Header>\n    <Card.Title>Workspace</Card.Title>\n    <Card.Description>Contexto operacional.</Card.Description>\n  </Card.Header>\n  <Card.Content>Conteúdo</Card.Content>\n</Card.Root>'
    },
    {
      slug: 'dialog',
      name: 'Dialog',
      category: 'Overlay',
      description: 'Modal acessível para confirmações e fluxos curtos.',
      code: 'import * as Dialog from "$lib/components/ui/dialog/index.js";\n\n<Dialog.Root>\n  <Dialog.Trigger>Abrir</Dialog.Trigger>\n  <Dialog.Content>\n    <Dialog.Header>\n      <Dialog.Title>Título</Dialog.Title>\n      <Dialog.Description>Descrição do modal.</Dialog.Description>\n    </Dialog.Header>\n  </Dialog.Content>\n</Dialog.Root>'
    },
    {
      slug: 'dropdown-menu',
      name: 'DropdownMenu',
      category: 'Overlay',
      description: 'Menu de ações contextual.',
      code: 'import * as DropdownMenu from "$lib/components/ui/dropdown-menu/index.js";\n\n<DropdownMenu.Root>\n  <DropdownMenu.Trigger>Ações</DropdownMenu.Trigger>\n  <DropdownMenu.Content>\n    <DropdownMenu.Item>Editar</DropdownMenu.Item>\n  </DropdownMenu.Content>\n</DropdownMenu.Root>'
    },
    {
      slug: 'popover',
      name: 'Popover',
      category: 'Overlay',
      description: 'Conteúdo contextual acionado por clique.',
      code: 'import * as Popover from "$lib/components/ui/popover/index.js";\n\n<Popover.Root>\n  <Popover.Trigger>Ajuda</Popover.Trigger>\n  <Popover.Content>Conteúdo do popover.</Popover.Content>\n</Popover.Root>'
    },
    {
      slug: 'tooltip',
      name: 'Tooltip',
      category: 'Overlay',
      description: 'Dica curta acionada por hover/foco.',
      code: 'import * as Tooltip from "$lib/components/ui/tooltip/index.js";\n\n<Tooltip.Provider>\n  <Tooltip.Root>\n    <Tooltip.Trigger>Hover</Tooltip.Trigger>\n    <Tooltip.Content>Texto de ajuda</Tooltip.Content>\n  </Tooltip.Root>\n</Tooltip.Provider>'
    },
    {
      slug: 'table',
      name: 'Table',
      category: 'Data',
      description: 'Tabela base para dados tabulares.',
      code: 'import * as Table from "$lib/components/ui/table/index.js";\n\n<Table.Root>\n  <Table.Header>\n    <Table.Row><Table.Head>Nome</Table.Head></Table.Row>\n  </Table.Header>\n  <Table.Body>\n    <Table.Row><Table.Cell>Noudoc</Table.Cell></Table.Row>\n  </Table.Body>\n</Table.Root>'
    },
    {
      slug: 'tabs',
      name: 'Tabs',
      category: 'Layout',
      description: 'Alternância entre painéis de conteúdo.',
      code: 'import * as Tabs from "$lib/components/ui/tabs/index.js";\n\n<Tabs.Root value="overview">\n  <Tabs.List>\n    <Tabs.Trigger value="overview">Overview</Tabs.Trigger>\n  </Tabs.List>\n  <Tabs.Content value="overview">Conteúdo</Tabs.Content>\n</Tabs.Root>'
    },
    {
      slug: 'empty',
      name: 'Empty',
      category: 'Feedback',
      description: 'Estado vazio para listas e telas sem dados.',
      code: 'import * as Empty from "$lib/components/ui/empty/index.js";\n\n<Empty.Root>\n  <Empty.Header>\n    <Empty.Title>Nenhum item</Empty.Title>\n    <Empty.Description>Crie o primeiro registro.</Empty.Description>\n  </Empty.Header>\n</Empty.Root>'
    },
    {
      slug: 'sidebar',
      name: 'Sidebar',
      category: 'Layout',
      description: 'Estrutura oficial para navegação lateral.',
      code: 'import * as Sidebar from "$lib/components/ui/sidebar/index.js";\n\n<Sidebar.Provider>\n  <Sidebar.Root>\n    <Sidebar.Header>Noudoc</Sidebar.Header>\n    <Sidebar.Content>Menu</Sidebar.Content>\n  </Sidebar.Root>\n  <Sidebar.Inset>Conteúdo</Sidebar.Inset>\n</Sidebar.Provider>'
    }
  ];

  let selected = $state('button');
  let checked = $state(true);
  let enabled = $state(true);
  let tab = $state('overview');
  let selectedRole = $state<string | undefined>('admin');

  const roles = [
    { label: 'Owner', value: 'owner' },
    { label: 'Admin', value: 'admin' },
    { label: 'Member', value: 'member' }
  ];

  const selectedRoleLabel = $derived(
    roles.find((item) => item.value === selectedRole)?.label ?? 'Selecione um perfil'
  );

  const active = $derived(componentDocs.find((component) => component.slug === selected) ?? componentDocs[0]);
</script>

<svelte:head>
  <title>Components | @noudoc/ui</title>
  <meta name="description" content="Painel de componentes oficiais shadcn-svelte usados no @noudoc/ui." />
</svelte:head>

<main class="min-h-screen bg-background text-foreground">
  <div class="mx-auto grid max-w-7xl gap-8 px-5 py-6 lg:grid-cols-[260px_minmax(0,1fr)]">
    <aside class="lg:sticky lg:top-6 lg:h-[calc(100vh-3rem)] lg:overflow-auto">
      <div class="rounded-xl border bg-card p-3 shadow-sm">
        <div class="border-b pb-3">
          <p class="text-xs font-medium uppercase tracking-wide text-muted-foreground">@noudoc/ui</p>
          <h1 class="mt-1 text-lg font-semibold tracking-tight">Components</h1>
        </div>

        <nav class="mt-3 grid gap-4">
          {#each [...new Set(componentDocs.map((component) => component.category))] as category}
            <div class="grid gap-1">
              <p class="px-2 text-xs font-medium text-muted-foreground">{category}</p>
              {#each componentDocs.filter((component) => component.category === category) as component}
                <button
                  type="button"
                  class="rounded-md px-2 py-1.5 text-left text-sm transition hover:bg-accent hover:text-accent-foreground {selected === component.slug ? 'bg-accent font-medium text-accent-foreground' : 'text-muted-foreground'}"
                  onclick={() => (selected = component.slug)}
                >
                  {component.name}
                </button>
              {/each}
            </div>
          {/each}
        </nav>
      </div>
    </aside>

    <section class="min-w-0 space-y-6">
      <div class="flex flex-col gap-3 border-b pb-6 sm:flex-row sm:items-end sm:justify-between">
        <div>
          <Badge variant="secondary">{active.category}</Badge>
          <h2 class="mt-3 text-3xl font-semibold tracking-tight">{active.name}</h2>
          <p class="mt-2 max-w-2xl text-sm text-muted-foreground">{active.description}</p>
        </div>
        <Button href="/">Voltar</Button>
      </div>

      <Card.Root>
        <Card.Header>
          <Card.Title>Preview</Card.Title>
          <Card.Description>Componente renderizado usando a implementação oficial instalada em `src/lib/components/ui`.</Card.Description>
        </Card.Header>
        <Card.Content>
          <div class="rounded-xl border bg-background p-6">
            {#if selected === 'button'}
              <div class="flex flex-wrap gap-2">
                <Button>Default</Button>
                <Button variant="secondary">Secondary</Button>
                <Button variant="outline">Outline</Button>
                <Button variant="ghost">Ghost</Button>
                <Button variant="destructive">Destructive</Button>
              </div>
            {:else if selected === 'input'}
              <div class="max-w-sm">
                <Input type="email" placeholder="admin@noudoc.com" value="admin@noudoc.com" />
              </div>
            {:else if selected === 'textarea'}
              <div class="max-w-lg">
                <Textarea placeholder="Digite uma observação para o workspace" />
              </div>
            {:else if selected === 'field'}
              <div class="max-w-md">
                <Field.Root>
                  <Field.Label>Nome do workspace</Field.Label>
                  <Input placeholder="Marketing" />
                  <Field.Description>Esse nome aparece no seletor principal do sistema.</Field.Description>
                </Field.Root>
              </div>
            {:else if selected === 'checkbox'}
              <div class="flex items-center gap-2">
                <Checkbox id="component-checkbox" bind:checked />
                <label for="component-checkbox" class="text-sm">Receber resumo diário</label>
              </div>
            {:else if selected === 'switch'}
              <div class="flex items-center gap-3">
                <Switch bind:checked={enabled} />
                <span class="text-sm">Modo autônomo {enabled ? 'ativo' : 'inativo'}</span>
              </div>
            {:else if selected === 'select'}
              <Select.Root type="single" bind:value={selectedRole}>
                <Select.Trigger class="w-[220px]">{selectedRoleLabel}</Select.Trigger>
                <Select.Content>
                  <Select.Group>
                    {#each roles as role}
                      <Select.Item value={role.value}>{role.label}</Select.Item>
                    {/each}
                  </Select.Group>
                </Select.Content>
              </Select.Root>
            {:else if selected === 'badge'}
              <div class="flex flex-wrap gap-2">
                <Badge>Default</Badge>
                <Badge variant="secondary">Secondary</Badge>
                <Badge variant="outline">Outline</Badge>
                <Badge variant="destructive">Destructive</Badge>
              </div>
            {:else if selected === 'card'}
              <Card.Root class="max-w-md">
                <Card.Header>
                  <Card.Title>Workspace</Card.Title>
                  <Card.Description>Contexto operacional da IA e das tarefas.</Card.Description>
                </Card.Header>
                <Card.Content>
                  <p class="text-sm text-muted-foreground">Use cards para agrupar blocos de informação e ações relacionadas.</p>
                </Card.Content>
              </Card.Root>
            {:else if selected === 'dialog'}
              <Dialog.Root>
                <Dialog.Trigger class="inline-flex h-9 items-center justify-center rounded-md bg-primary px-4 py-2 text-sm font-medium text-primary-foreground shadow-xs hover:bg-primary/90">Abrir modal</Dialog.Trigger>
                <Dialog.Content>
                  <Dialog.Header>
                    <Dialog.Title>Arquivar workspace?</Dialog.Title>
                    <Dialog.Description>Essa ação pode ser revertida depois.</Dialog.Description>
                  </Dialog.Header>
                  <Dialog.Footer>
                    <Dialog.Close class="inline-flex h-9 items-center justify-center rounded-md border px-4 py-2 text-sm font-medium shadow-xs">Cancelar</Dialog.Close>
                    <Button variant="destructive">Arquivar</Button>
                  </Dialog.Footer>
                </Dialog.Content>
              </Dialog.Root>
            {:else if selected === 'dropdown-menu'}
              <DropdownMenu.Root>
                <DropdownMenu.Trigger class="inline-flex h-9 items-center justify-center rounded-md border px-4 py-2 text-sm font-medium shadow-xs">Ações</DropdownMenu.Trigger>
                <DropdownMenu.Content>
                  <DropdownMenu.Label>Workspace</DropdownMenu.Label>
                  <DropdownMenu.Item>Editar</DropdownMenu.Item>
                  <DropdownMenu.Item>Duplicar</DropdownMenu.Item>
                  <DropdownMenu.Separator />
                  <DropdownMenu.Item variant="destructive">Excluir</DropdownMenu.Item>
                </DropdownMenu.Content>
              </DropdownMenu.Root>
            {:else if selected === 'popover'}
              <Popover.Root>
                <Popover.Trigger class="inline-flex h-9 items-center justify-center rounded-md border px-4 py-2 text-sm font-medium shadow-xs">Abrir popover</Popover.Trigger>
                <Popover.Content class="w-72">
                  <Popover.Header>
                    <Popover.Title>Dica rápida</Popover.Title>
                    <Popover.Description>Use popover para conteúdo curto e contextual.</Popover.Description>
                  </Popover.Header>
                </Popover.Content>
              </Popover.Root>
            {:else if selected === 'tooltip'}
              <Tooltip.Provider>
                <Tooltip.Root>
                  <Tooltip.Trigger class="inline-flex h-9 items-center justify-center rounded-md border px-4 py-2 text-sm font-medium shadow-xs">Passe o mouse</Tooltip.Trigger>
                  <Tooltip.Content>Ajuda contextual curta</Tooltip.Content>
                </Tooltip.Root>
              </Tooltip.Provider>
            {:else if selected === 'table'}
              <Table.Root>
                <Table.Header>
                  <Table.Row>
                    <Table.Head>Workspace</Table.Head>
                    <Table.Head>Status</Table.Head>
                    <Table.Head class="text-right">Tarefas</Table.Head>
                  </Table.Row>
                </Table.Header>
                <Table.Body>
                  <Table.Row>
                    <Table.Cell>Marketing</Table.Cell>
                    <Table.Cell><Badge variant="secondary">Ativo</Badge></Table.Cell>
                    <Table.Cell class="text-right">24</Table.Cell>
                  </Table.Row>
                  <Table.Row>
                    <Table.Cell>Comercial</Table.Cell>
                    <Table.Cell><Badge variant="outline">Rascunho</Badge></Table.Cell>
                    <Table.Cell class="text-right">8</Table.Cell>
                  </Table.Row>
                </Table.Body>
              </Table.Root>
            {:else if selected === 'tabs'}
              <Tabs.Root bind:value={tab}>
                <Tabs.List>
                  <Tabs.Trigger value="overview">Overview</Tabs.Trigger>
                  <Tabs.Trigger value="settings">Settings</Tabs.Trigger>
                </Tabs.List>
                <Tabs.Content value="overview" class="rounded-md border p-4 text-sm text-muted-foreground">Resumo do workspace.</Tabs.Content>
                <Tabs.Content value="settings" class="rounded-md border p-4 text-sm text-muted-foreground">Configurações do workspace.</Tabs.Content>
              </Tabs.Root>
            {:else if selected === 'empty'}
              <Empty.Root>
                <Empty.Header>
                  <Empty.Title>Nenhum registro encontrado</Empty.Title>
                  <Empty.Description>Crie o primeiro item para começar.</Empty.Description>
                </Empty.Header>
                <Empty.Content>
                  <Button>Criar item</Button>
                </Empty.Content>
              </Empty.Root>
            {:else if selected === 'sidebar'}
              <div class="overflow-hidden rounded-lg border">
                <Sidebar.Provider class="min-h-[320px]">
                  <Sidebar.Root collapsible="none">
                    <Sidebar.Header>
                      <div class="px-2 py-1 text-sm font-semibold">Noudoc</div>
                    </Sidebar.Header>
                    <Sidebar.Content>
                      <Sidebar.Group>
                        <Sidebar.GroupLabel>Menu</Sidebar.GroupLabel>
                        <Sidebar.GroupContent>
                          <Sidebar.Menu>
                            <Sidebar.MenuItem>
                              <Sidebar.MenuButton>Dashboard</Sidebar.MenuButton>
                            </Sidebar.MenuItem>
                            <Sidebar.MenuItem>
                              <Sidebar.MenuButton>Workspaces</Sidebar.MenuButton>
                            </Sidebar.MenuItem>
                          </Sidebar.Menu>
                        </Sidebar.GroupContent>
                      </Sidebar.Group>
                    </Sidebar.Content>
                  </Sidebar.Root>
                  <Sidebar.Inset class="p-4">
                    <p class="text-sm text-muted-foreground">Área de conteúdo ao lado da sidebar.</p>
                  </Sidebar.Inset>
                </Sidebar.Provider>
              </div>
            {/if}
          </div>
        </Card.Content>
      </Card.Root>

      <Card.Root>
        <Card.Header>
          <Card.Title>Como usar</Card.Title>
          <Card.Description>Exemplo mínimo para copiar no projeto.</Card.Description>
        </Card.Header>
        <Card.Content>
          <pre class="overflow-auto rounded-lg bg-muted p-4 text-sm leading-6"><code>{active.code}</code></pre>
        </Card.Content>
      </Card.Root>
    </section>
  </div>
</main>
