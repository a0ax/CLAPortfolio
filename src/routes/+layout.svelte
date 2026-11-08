<script>
  import { page } from '$app/state';

  let { children } = $props();

  const entries = [
    { href: '/experience', name: 'experience/' },
    { href: '/portfolio', name: 'portfolio/' },
    { href: '/contact', name: 'contact/' }
  ];

  const here = $derived(page.url.pathname.replace(/\/$/, '') || '/');
</script>

<svelte:head>
  <title>{here === '/' ? 'home' : here.slice(1)}</title>
</svelte:head>

<main>
  <p>~{here === '/' ? '' : here}$ ls</p>

  <ul>
    {#if here !== '/'}
      <li><a href="/">../</a></li>
    {/if}
    {#each entries as e}
      <li>
        <a href={e.href} aria-current={here === e.href ? 'page' : undefined}>{e.name}</a>
      </li>
    {/each}
  </ul>

  <hr />

  {@render children()}
</main>

<style>
  :global(body) {
    font-family: ui-monospace, 'SFMono-Regular', Menlo, Consolas, monospace;
    max-width: 60ch;
    margin: 2rem auto;
    padding: 0 1rem;
    line-height: 1.5;
  }
  ul {
    list-style: none;
    padding: 0;
    margin: 0;
  }
  a[aria-current='page'] {
    font-weight: bold;
    text-decoration: none;
  }
</style>
