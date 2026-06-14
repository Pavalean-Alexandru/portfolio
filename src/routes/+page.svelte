<script>
  import { base } from '$app/paths';
  import { onMount } from 'svelte';
  let visible = $state(false);
  onMount(() => {
    setTimeout(() => { visible = true; }, 100);
  });
</script>

<svelte:head>
  <title>Alexandru Pavalean — Portfolio</title>
</svelte:head>

<section class="hero" class:visible>
  <div class="hero-top">
    <p class="label">PORTFOLIO DIGITALE · 2023–2026</p>
  </div>

  <div class="hero-name">
    <h1>Alexandru<br />Pavalean</h1>
  </div>

  <p class="subtitle">STUDENTE · ISTITUTO EDOARDO AGNELLI</p>

  <div class="hero-cta">
    <a href="{base}/chi-sono" class="btn btn-solid">CHI SONO →</a>
    <a href="{base}/progetti" class="btn btn-outline">PROGETTI →</a>
  </div>

  <div class="hero-stats">
    <div class="stat-group">
      <span class="stat-item">3 ANNI</span>
      <span class="dot">·</span>
      <span class="stat-item">9 PROGETTI</span>
    </div>
  </div>
</section>

<style>
  .hero {
    min-height: calc(100vh - 4rem);
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding: 4rem 2rem 2rem;
    max-width: 1200px;
    margin: 0 auto;
    opacity: 0;
    transition: opacity 0.6s;
  }

  .hero.visible { opacity: 1; }

  .label {
    font-size: 0.7rem;
    letter-spacing: 0.15em;
    color: var(--fg-muted);
    margin-bottom: 1rem;
  }

  h1 {
    font-family: var(--font-serif);
    font-size: clamp(5rem, 14vw, 12rem);
    font-weight: 900;
    line-height: 0.9;
    letter-spacing: -0.02em;
    margin-bottom: 1rem;
  }

  .subtitle {
    font-size: 0.7rem;
    letter-spacing: 0.15em;
    color: var(--fg-muted);
    margin-bottom: 2.5rem;
  }

  .hero-cta {
    display: flex;
    gap: 1rem;
    flex-wrap: wrap;
    margin-bottom: 4rem;
  }

  .btn {
    display: inline-flex;
    align-items: center;
    padding: 0.875rem 1.75rem;
    font-size: 0.7rem;
    letter-spacing: 0.12em;
    font-weight: 500;
    transition: all 0.2s;
    font-family: var(--font-sans);
  }

  .btn-solid { background: var(--fg); color: var(--bg); }
  .btn-solid:hover { background: var(--accent); }
  .btn-outline { border: 1px solid var(--fg); color: var(--fg); }
  .btn-outline:hover { background: var(--fg); color: var(--bg); }

  .hero-stats {
    padding-top: 1.5rem;
    border-top: 1px solid var(--border);
  }

  .stat-group {
    display: flex;
    align-items: center;
    gap: 0.75rem;
  }

  .stat-item {
    font-size: 0.68rem;
    letter-spacing: 0.1em;
    color: var(--fg-muted);
  }

  .dot { color: var(--fg-muted); }
</style>