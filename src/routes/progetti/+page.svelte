<script>
  import { onMount } from 'svelte';
  let visible = $state(false);
  let hoveredYear = $state(null);

  const anni = [
    {
      anno: 3,
      titolo: 'Terzo Superiore',
      periodo: '2023 – 2024',
      progetti: [
        { materia: 'Italiano', titolo: 'La Mattanza', descrizione: 'Analisi del tema della mattanza, tradizione della pesca al tonno nella cultura siciliana.', tipo: 'Testo / Analisi' },
        { materia: 'Informatica', titolo: 'Codice Fiscale', descrizione: 'Programma per il calcolo e la verifica del codice fiscale italiano.', tipo: 'Programmazione' },
        { materia: 'Storia', titolo: 'Zoomafia', descrizione: 'Presentazione sul fenomeno della zoomafia in Italia e il legame con la criminalità organizzata.', tipo: 'Presentazione' }
      ],
      discipline: ['Italiano', 'Informatica', 'Storia']
    },
    {
      anno: 4,
      titolo: 'Quarto Superiore',
      periodo: '2024 – 2025',
      progetti: [
        { materia: 'Informatica', titolo: 'Quiz della Patente', descrizione: 'Applicazione web per la simulazione dell\'esame della patente di guida.', tipo: 'Applicazione Web' },
        { materia: 'Storia', titolo: 'Popoli Antichi', descrizione: 'Presentazione sullo studio dei popoli dell\'antichità e delle loro civiltà.', tipo: 'Presentazione' }
      ],
      discipline: ['Informatica', 'Storia']
    },
    {
      anno: 5,
      titolo: 'Quinto Superiore',
      periodo: '2025 – 2026',
      progetti: [
        { materia: 'Informatica', titolo: '1522 — Antiviolenza', descrizione: 'Progetto web dedicato al numero antiviolenza 1522 con risorse informative.', tipo: 'Applicazione Web' },
        { materia: 'Italiano', titolo: 'Prigione Domestica', descrizione: 'Analisi letteraria sul tema della prigionia domestica e la condizione femminile.', tipo: 'Testo / Analisi' },
        { materia: 'Sistemi', titolo: 'Cybersecurity', descrizione: 'Studio delle principali minacce informatiche e tecniche di protezione dei sistemi.', tipo: 'Ricerca Tecnica' },
        { materia: 'Storia', titolo: 'Il Nazismo', descrizione: 'Approfondimento storico sull\'ascesa del nazismo e le sue conseguenze.', tipo: 'Ricerca Storica' }
      ],
      discipline: ['Informatica', 'Italiano', 'Sistemi', 'Storia']
    }
  ];

  onMount(() => {
    setTimeout(() => { visible = true; }, 100);
  });
</script>

<svelte:head>
  <title>Progetti — Alexandru Pavalean</title>
</svelte:head>

<div class="page" class:visible>
  <div class="page-header">
    <div>
      <p class="label">02 — ARCHIVIO</p>
      <h1>Progetti<span class="accent">.</span></h1>
    </div>
    <p class="meta">9 progetti · 3 anni</p>
  </div>

  <div class="divider"></div>

  {#each anni as anno, i}
    <div
  class="anno-row"
  class:hovered={hoveredYear === anno.anno}
  onmouseenter={() => hoveredYear = anno.anno}
  onmouseleave={() => hoveredYear = null}
>
      <div class="anno-left">
        <span class="anno-num">{anno.anno}°</span>
        <div class="anno-info">
          <h2 class="anno-title">{anno.titolo}</h2>
          <p class="anno-meta">{anno.periodo} · {anno.progetti.length} PROGETTI</p>
        </div>
      </div>

      <div class="anno-tags">
        {#each anno.discipline as disc}
          <span class="tag" class:tag-accent={disc === 'Informatica' || disc === 'Sistemi'}>{disc}</span>
        {/each}
      </div>

      <div class="anno-arrow">→</div>

      <div class="progetti-expanded">
        {#each anno.progetti as prog}
          <div class="prog-item">
            <div class="prog-materia">{prog.materia}</div>
            <h3 class="prog-title">{prog.titolo}</h3>
            <p class="prog-desc">{prog.descrizione}</p>
            <span class="prog-tipo">{prog.tipo}</span>
          </div>
        {/each}
      </div>
    </div>

    <div class="divider"></div>
  {/each}

  <div class="page-footer">
    <p>Istituto Edoardo Agnelli · Torino · 2023–2026</p>
    <a href="/chi-sono" class="footer-link">← Chi Sono</a>
  </div>
</div>

<style>
  .page {
    max-width: 1200px;
    margin: 0 auto;
    padding: 2rem 2rem 4rem;
    opacity: 0;
    transition: opacity 0.6s;
  }

  .page.visible { opacity: 1; }

  .page-header {
    display: flex;
    align-items: flex-end;
    justify-content: space-between;
    padding-bottom: 1.5rem;
  }

  .label { font-size: 0.68rem; letter-spacing: 0.12em; color: var(--fg-muted); margin-bottom: 0.25rem; }

  h1 { font-family: var(--font-serif); font-size: clamp(2.5rem, 6vw, 4rem); font-weight: 700; letter-spacing: -0.02em; line-height: 1; }
  .accent { color: var(--accent); }
  .meta { font-size: 0.68rem; letter-spacing: 0.1em; color: var(--fg-muted); padding-bottom: 0.5rem; }

  .divider { height: 1px; background: var(--border); }

  .anno-row {
    padding: 2rem 0;
    display: grid;
    grid-template-columns: 1fr auto auto;
    align-items: center;
    gap: 2rem;
    overflow: hidden;
  }

  .anno-left { display: flex; align-items: center; gap: 2rem; }

  .anno-num {
    font-family: var(--font-serif);
    font-size: 4rem;
    font-weight: 900;
    color: var(--border);
    line-height: 1;
    min-width: 3rem;
    text-align: center;
    transition: color 0.3s;
    user-select: none;
  }

  .anno-row.hovered .anno-num { color: #ccc; }

  .anno-title { font-family: var(--font-serif); font-size: 1.6rem; font-weight: 700; transition: color 0.2s; }
  .anno-row.hovered .anno-title { color: var(--accent); }

  .anno-meta { font-size: 0.65rem; letter-spacing: 0.12em; color: var(--fg-muted); margin-top: 0.35rem; }

  .anno-tags { display: flex; gap: 0.5rem; flex-wrap: wrap; justify-content: flex-end; max-width: 250px; }

  .tag { padding: 0.25rem 0.6rem; font-size: 0.62rem; letter-spacing: 0.08em; border: 1px solid var(--border); color: var(--fg-muted); white-space: nowrap; }
  .tag.tag-accent { border-color: var(--accent); color: var(--accent); }

  .anno-arrow {
    width: 2rem; height: 2rem;
    border: 1px solid var(--border);
    border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    font-size: 0.8rem; color: var(--fg-muted);
    transition: all 0.3s;
    flex-shrink: 0;
  }

  .anno-row.hovered .anno-arrow { background: var(--fg); color: var(--bg); border-color: var(--fg); transform: rotate(45deg); }

  .progetti-expanded {
    grid-column: 1 / -1;
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
    gap: 1rem;
    max-height: 0;
    overflow: hidden;
    opacity: 0;
    transition: max-height 0.5s cubic-bezier(0.16, 1, 0.3, 1), opacity 0.3s ease, padding 0.3s;
  }

  .anno-row.hovered .progetti-expanded { max-height: 600px; opacity: 1; padding-top: 1rem; }

  .prog-item {
    border: 1px solid var(--border);
    padding: 1.25rem;
    background: var(--white);
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    transition: border-color 0.2s, transform 0.2s;
  }

  .prog-item:hover { border-color: var(--fg-muted); transform: translateY(-2px); }

  .prog-materia { font-size: 0.6rem; letter-spacing: 0.15em; color: var(--accent); font-weight: 500; text-transform: uppercase; }
  .prog-title { font-family: var(--font-serif); font-size: 1.1rem; font-weight: 700; }
  .prog-desc { font-size: 0.8rem; line-height: 1.6; color: var(--fg-muted); font-weight: 300; }
  .prog-tipo { display: inline-block; font-size: 0.58rem; letter-spacing: 0.1em; padding: 0.2rem 0.5rem; border: 1px solid var(--border); color: var(--fg-muted); align-self: flex-start; margin-top: auto; }

  .page-footer {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-top: 3rem;
    padding-top: 1.5rem;
    border-top: 1px solid var(--border);
  }

  .page-footer p { font-size: 0.65rem; letter-spacing: 0.1em; color: var(--fg-muted); }
  .footer-link { font-size: 0.65rem; letter-spacing: 0.1em; color: var(--fg-muted); transition: color 0.2s; }
  .footer-link:hover { color: var(--fg); }

  @media (max-width: 768px) {
    .anno-row { grid-template-columns: 1fr; }
    .anno-tags { justify-content: flex-start; max-width: none; }
    .anno-arrow { display: none; }
  }
</style>