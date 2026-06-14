<script>
  import '../app.css';
  import { page } from '$app/stores';
  import { base } from '$app/paths';

  let { children } = $props();
  let menuOpen = $state(false);

  function toggleMenu() {
    menuOpen = !menuOpen;
  }

  function closeMenu() {
    menuOpen = false;
  }

  function goBack() {
    history.back();
  }
</script>

<header>
  <div class="header-left">
    {#if $page.url.pathname === `${base}/` || $page.url.pathname === base}
    {:else}
      <button class="back-btn" onclick={goBack}>
        ← INDIETRO
      </button>
    {/if}
  </div>

  <button class="menu-btn" onclick={toggleMenu}>
    {#if menuOpen}✕{:else}☰{/if}
  </button>
</header>

{#if menuOpen}
  <div class="menu-overlay" role="button" tabindex="0" onclick={closeMenu} onkeydown={closeMenu}>
    <nav class="menu-nav">
      <button class="menu-close" onclick={closeMenu}>✕</button>
      <ul>
        <li><a href="{base}/" onclick={closeMenu}>Home</a></li>
        <li><a href="{base}/chi-sono" onclick={closeMenu}>Chi Sono</a></li>
        <li><a href="{base}/progetti" onclick={closeMenu}>Progetti</a></li>
      </ul>
      <div class="menu-footer">
        <span>Alexandru Pavalean</span>
        <span>Istituto Edoardo Agnelli</span>
      </div>
    </nav>
  </div>
{/if}

<main>
  {@render children()}
</main>

<style>
  header {
    position: fixed;
    top: 0; left: 0; right: 0;
    z-index: 100;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 1.25rem 2rem;
    background: var(--bg);
  }

  .logo { font-family: var(--font-sans); font-weight: 500; font-size: 1rem; color: var(--fg); }

  .back-btn { font-family: var(--font-sans); font-size: 0.75rem; letter-spacing: 0.1em; color: var(--fg); transition: opacity 0.2s; font-weight: 400; }
  .back-btn:hover { opacity: 0.6; }

  .menu-btn { font-size: 1.2rem; color: var(--fg); width: 2.5rem; height: 2.5rem; border: 1px solid var(--border); display: flex; align-items: center; justify-content: center; transition: background 0.2s; }
  .menu-btn:hover { background: var(--fg); color: var(--bg); }

  .menu-overlay { position: fixed; inset: 0; z-index: 200; background: rgba(26,26,26,0.5); backdrop-filter: blur(2px); }

  .menu-nav { position: absolute; top: 0; right: 0; bottom: 0; width: 320px; background: var(--fg); color: var(--bg); padding: 2rem; display: flex; flex-direction: column; }

  .menu-close { color: var(--bg); font-size: 1.1rem; align-self: flex-end; margin-bottom: 3rem; opacity: 0.6; }
  .menu-close:hover { opacity: 1; }

  ul { list-style: none; flex: 1; }
  ul li { border-bottom: 1px solid rgba(255,255,255,0.1); }
  ul li a { display: block; padding: 1.25rem 0; font-family: var(--font-serif); font-size: 1.75rem; color: var(--bg); transition: opacity 0.2s; }
  ul li a:hover { opacity: 0.6; }

  .menu-footer { display: flex; flex-direction: column; gap: 0.25rem; font-size: 0.7rem; letter-spacing: 0.08em; opacity: 0.4; text-transform: uppercase; }

  main { padding-top: 4rem; }
</style>