<script>
  import { base } from '$app/paths';
  import { onMount } from 'svelte';
  let visible = $state(false);
  let activeTab = $state(1);

  const tabs = [
    { id: 1, content: 'Mi chiamo Alexandru Pavalean, ho 18 anni e sono uno studente dell\'Istituto Edoardo Agnelli di Torino. Sono un ragazzo tranquillo e collaborativo, sempre disponibile a lavorare in gruppo e ad affrontare nuove sfide con impegno e serietà.' },
    { id: 2, content: 'Frequento il quinto anno dell\'istituto tecnico, indirizzo informatica e telecomunicazioni. In questi tre anni ho sviluppato competenze in programmazione, sistemi informatici.' },
    { id: 3, content: 'Sono motivato a crescere nel campo dell\'informatica e della tecnologia. Voglio continuare a formarmi e mettere a frutto le competenze acquisite durante il percorso scolastico.' }
  ];

  const passioni = [
    { emoji: '🎵', label: 'MUSICA' },
    { emoji: '⚽', label: 'CALCIO' },
    { emoji: '🎬', label: 'FILM' }
  ];

  onMount(() => {
    setTimeout(() => { visible = true; }, 100);
  });
</script>

<svelte:head>
  <title>Chi Sono — Alexandru Pavalean</title>
</svelte:head>

<div class="page" class:visible>
  <div class="image-col">
    <div class="image-placeholder">
      <svg viewBox="0 0 400 500" fill="none" xmlns="http://www.w3.org/2000/svg">
        <rect width="400" height="500" fill="#2a2a2a"/>
        <circle cx="200" cy="160" r="70" fill="#444"/>
        <ellipse cx="200" cy="380" rx="120" ry="80" fill="#444"/>
      </svg>
    </div>
    <div class="stats-grid">
      <div class="stat-card"><div class="stat-num">3</div><div class="stat-lbl">ANNI</div></div>
      <div class="stat-card"><div class="stat-num">9</div><div class="stat-lbl">PROGETTI</div></div>
      <div class="stat-card"><div class="stat-num">5</div><div class="stat-lbl">DISCIPLINE</div></div>
    </div>
  </div>

  <div class="content-col">
    <div class="section-label">
      <span class="dot-red">●</span>
      <span>CHI SONO</span>
    </div>

    <h1 class="section-title">Chi Sono<span class="accent">.</span></h1>

    <div class="tabs">
      {#each tabs as tab}
        <button class="tab-btn" class:active={activeTab === tab.id} onclick={() => activeTab = tab.id}>
          0{tab.id}
        </button>
      {/each}
    </div>

    <div class="tab-content">
      {#each tabs as tab}
        {#if activeTab === tab.id}
          <p class="bio-text">{tab.content}</p>
        {/if}
      {/each}
    </div>

    <div class="passioni-section">
      <p class="passioni-label">PASSIONI</p>
      <div class="passioni-list">
        {#each passioni as p}
          <div class="passione-chip">
            <span>{p.emoji}</span>
            <span>{p.label}</span>
          </div>
        {/each}
      </div>
    </div>

    <a href="{base}/progetti" class="cta-btn">ESPLORA I PROGETTI →</a>
  </div>
</div>

<style>
  .page {
    display: grid;
    grid-template-columns: 1fr 1fr;
    height: calc(100vh - 4rem);
    overflow: hidden;
    opacity: 0;
    transition: opacity 0.6s;
  }

  .page.visible { opacity: 1; }

  .image-col { background: #1a1a1a; display: flex; flex-direction: column; height: 100%; overflow: hidden; }

  .image-placeholder { flex: 1; overflow: hidden; }
  .image-placeholder svg { width: 100%; height: 100%; display: block; object-fit: cover; }

  .stats-grid { display: grid; grid-template-columns: repeat(3, 1fr); }

  .stat-card { padding: 1.25rem 1rem; background: #111; border-top: 1px solid #2a2a2a; border-right: 1px solid #2a2a2a; }
  .stat-card:last-child { border-right: none; }

  .stat-num { font-family: var(--font-serif); font-size: 2rem; font-weight: 900; color: #fff; line-height: 1; }
  .stat-lbl { font-size: 0.6rem; letter-spacing: 0.12em; color: rgba(255,255,255,0.4); margin-top: 0.25rem; }

  .content-col { padding: 1.5rem 2.5rem; display: flex; flex-direction: column; justify-content: center; gap: 1rem; overflow-y: auto; }

  .section-label { display: flex; align-items: center; gap: 0.5rem; font-size: 0.65rem; letter-spacing: 0.15em; color: var(--fg-muted); }
  .dot-red { color: var(--accent); font-size: 0.5rem; }

  .section-title { font-family: var(--font-serif); font-size: clamp(2.5rem, 4vw, 3.5rem); font-weight: 700; line-height: 1; }
  .accent { color: var(--accent); }

  .tabs { display: flex; gap: 0.5rem; }

  .tab-btn { padding: 0.4rem 0.75rem; font-size: 0.7rem; font-family: var(--font-sans); color: var(--fg-muted); border: 1px solid var(--border); transition: all 0.2s; background: transparent; }
  .tab-btn.active { background: var(--fg); color: var(--bg); border-color: var(--fg); }

  .bio-text { font-size: 1.1rem; line-height: 1.75; color: var(--fg); font-weight: 300; }

  .passioni-label { font-size: 0.65rem; letter-spacing: 0.15em; color: var(--fg-muted); }

  .passioni-list { display: flex; gap: 0.75rem; flex-wrap: wrap; }

  .passione-chip { display: flex; align-items: center; gap: 0.5rem; padding: 0.5rem 1rem; border: 1px solid var(--border); font-size: 0.7rem; letter-spacing: 0.1em; transition: all 0.2s; }
  .passione-chip:hover { border-color: var(--fg); background: var(--fg); color: var(--bg); }

  .cta-btn { display: inline-flex; align-items: center; background: var(--fg); color: var(--bg); padding: 1rem 2rem; font-size: 0.7rem; letter-spacing: 0.12em; font-weight: 500; align-self: flex-start; transition: background 0.2s; }
  .cta-btn:hover { background: var(--accent); }

  @media (max-width: 768px) {
    .page { grid-template-columns: 1fr; }
    .content-col { padding: 2rem 1.5rem; }
  }
</style>