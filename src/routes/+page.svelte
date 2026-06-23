<svelte:head>
  <title>@noudoc/ui</title>
  <meta name="description" content="Noudoc UI kit based on official shadcn-svelte components." />
</svelte:head>

<main class="mx-auto grid min-h-screen max-w-3xl place-items-center px-6 py-16">
  <section class="grid gap-4 text-center">
    <p class="text-sm font-medium text-muted-foreground">Noudoc Design System</p>
    <h1 class="text-4xl font-semibold tracking-tight">@noudoc/ui</h1>
    <p class="text-muted-foreground">
      Projeto limpo para usar componentes oficiais do shadcn-svelte e componentes próprios Noudoc separados.
    </p>

    <div class="mt-2 flex flex-wrap justify-center gap-2">
      <a class="inline-flex h-9 items-center justify-center rounded-md bg-primary px-4 py-2 text-sm font-medium text-primary-foreground shadow-xs hover:bg-primary/90" href="/components">
        Ver componentes oficiais
      </a>
      <a class="inline-flex h-9 items-center justify-center rounded-md border px-4 py-2 text-sm font-medium shadow-xs hover:bg-accent hover:text-accent-foreground" href="/noudoc">
        Ver componentes Noudoc
      </a>
      <a class="inline-flex h-9 items-center justify-center rounded-md border px-4 py-2 text-sm font-medium shadow-xs hover:bg-accent hover:text-accent-foreground" href="https://www.shadcn-svelte.com/docs/components" target="_blank" rel="noreferrer">
        Docs shadcn
      </a>
    </div>

    <pre class="mt-4 overflow-auto rounded-lg border bg-muted p-4 text-left text-sm"><code>npm run check
npm run build
npm run dev</code></pre>
  </section>
</main>
