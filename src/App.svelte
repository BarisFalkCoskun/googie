<script>
  import { onMount } from 'svelte';
  import { tweened } from 'svelte/motion';
  import { cubicOut } from 'svelte/easing';
  import { fade, fly, scale, draw } from 'svelte/transition';
  import { flip } from 'svelte/animate';

  let menuOpen = false;

  function toggleMenu() {
    menuOpen = !menuOpen;
  }

  function closeMenu() {
    menuOpen = false;
  }

  const boardMessages = [
    'Signal open for new collaborations',
    'Design from the street, not a template',
    'Googie geometry + modern UX',
    'Motion cues beat empty whitespace',
    'Color is a wayfinding system'
  ];

  const themes = [
    {
      name: 'Neon',
      accent: '#32c6c2',
      accentTwo: '#ff6b57',
      beam: '#ffc857'
    },
    {
      name: 'Desert',
      accent: '#ffc857',
      accentTwo: '#ff8f62',
      beam: '#32c6c2'
    },
    {
      name: 'Noir',
      accent: '#3dd9b3',
      accentTwo: '#f7c66f',
      beam: '#c7d7e1'
    }
  ];

  let themeChoice = themes[0];
  let boardIndex = 0;
  let boardMessage = boardMessages[0];

  let powerControl = 72;
  let hueShift = 0;
  let tilt = -6;

  const signalPower = tweened(powerControl, { duration: 500, easing: cubicOut });
  $: signalPower.set(powerControl);

  const stats = [
    { label: 'Visual Systems', target: 18, suffix: '+' },
    { label: 'Motion Toolkits', target: 12, suffix: '' },
    { label: 'Field Drives', target: 24, suffix: '' }
  ];

  const statStores = stats.map(() => tweened(0, { duration: 1200, easing: cubicOut }));
  let statValues = stats.map(() => 0);
  let statUnsubs = [];

  const principles = [
    {
      title: 'Borrow the real world',
      copy: 'Signs, tickets, terrazzo floors, and road maps are fair game online.',
      tag: 'Material'
    },
    {
      title: 'Geometry with optimism',
      copy: 'Boomerangs, starbursts, and angled roofs create motion without noise.',
      tag: 'Form'
    },
    {
      title: 'Color as navigation',
      copy: 'Neon and sunlit palettes guide attention like street lighting.',
      tag: 'Guidance'
    },
    {
      title: 'Motion as a cue',
      copy: 'Sweeps, pulses, and marquee rhythms show the next step.',
      tag: 'Motion'
    }
  ];

  const projects = [
    {
      name: 'Signal Atlas',
      role: 'Product design',
      desc: 'A map of night routes that turns city data into glowing wayfinding.',
      tags: ['Web', 'Mapping'],
      type: 'Product',
      year: 2024
    },
    {
      name: 'Orbit Planner',
      role: 'Interaction design',
      desc: 'A scheduling tool for studios that treats time like a runway.',
      tags: ['Systems', 'SaaS'],
      type: 'Systems',
      year: 2023
    },
    {
      name: 'Neon Specimen',
      role: 'Visual system',
      desc: 'A type exploration that mixes signage, tickets, and hand-lettering.',
      tags: ['Identity', 'Type'],
      type: 'Identity',
      year: 2022
    },
    {
      name: 'Drive-In Toolkit',
      role: 'Creative code',
      desc: 'Reusable motion patterns inspired by roadside signage and travel boards.',
      tags: ['Motion', 'UI'],
      type: 'Motion',
      year: 2024
    },
    {
      name: 'Panorama Kiosk',
      role: 'UX strategy',
      desc: 'A retail touch screen flow that mimics airport terminal cues.',
      tags: ['UX', 'Hardware'],
      type: 'Product',
      year: 2021
    },
    {
      name: 'Starburst Identity',
      role: 'Brand system',
      desc: 'A modular identity built around burst geometry and neon contrast.',
      tags: ['Identity', 'Brand'],
      type: 'Identity',
      year: 2023
    }
  ];

  const experiments = [
    {
      title: 'Starburst Generator',
      format: 'SVG tool',
      desc: 'Builds retro bursts with adjustable rays and glow layers.',
      detail: 'Uses dynamic SVG math to keep angles crisp at any size.'
    },
    {
      title: 'Ticket Stub UI',
      format: 'Component study',
      desc: 'Explores clipped corners, embossing, and ink-stamp textures.',
      detail: 'Reusable tokens for cards, forms, and micro panels.'
    },
    {
      title: 'Runway Lightline',
      format: 'Motion loop',
      desc: 'A looping guide rail animation for navigation cues.',
      detail: 'Tunable speed, density, and glow intensity.'
    }
  ];

  const studioSteps = [
    {
      title: 'Collect the cues',
      desc: 'Photograph signage, watch traffic flow, archive ephemera.'
    },
    {
      title: 'Translate the forms',
      desc: 'Turn real-world geometry into scalable UI structures.'
    },
    {
      title: 'Tune the signal',
      desc: 'Use motion and color to guide without overwhelming.'
    }
  ];

  const timeline = [
    {
      year: '2018',
      title: 'Started building Googie-inspired UI studies.',
      detail: 'Collected signage and roadside forms across the west coast.'
    },
    {
      year: '2020',
      title: 'Launched visual systems for two travel startups.',
      detail: 'Focused on navigation-heavy interfaces and wayfinding.'
    },
    {
      year: '2022',
      title: 'Opened a small studio for motion and interaction.',
      detail: 'Built toolkits for ticketing, signage, and glow effects.'
    },
    {
      year: '2024',
      title: 'Exploring multi-style web experiences for personal brands.',
      detail: 'Combining architecture, print, and motion into websites.'
    }
  ];

  const nowItems = [
    'Designing a web identity for a community airfield.',
    'Prototyping a motion system based on runways and checklists.',
    'Open for select collaborations in 2025.'
  ];

  const links = [
    { label: 'Email', value: 'hello@coskun.studio' },
    { label: 'Portfolio', value: 'coskun.studio' },
    { label: 'Github', value: 'github.com/coskun' }
  ];

  const filters = ['All', 'Product', 'Identity', 'Motion', 'Systems'];
  const sortModes = ['Newest', 'Alphabet'];

  let activeFilter = 'All';
  let sortMode = 'Newest';
  let openExperiment = experiments[0].title;

  $: filteredProjects =
    activeFilter === 'All'
      ? projects
      : projects.filter((project) => project.type === activeFilter);

  $: sortedProjects = [...filteredProjects].sort((a, b) =>
    sortMode === 'Newest' ? b.year - a.year : a.name.localeCompare(b.name)
  );

  $: huePercent = Math.round(((hueShift + 30) / 60) * 100);
  $: tiltPercent = Math.round(((tilt + 15) / 30) * 100);

  const noop = () => {};

  onMount(() => {
    const id = setInterval(() => {
      boardIndex = (boardIndex + 1) % boardMessages.length;
      boardMessage = boardMessages[boardIndex];
    }, 2400);

    statUnsubs = statStores.map((store, index) =>
      store.subscribe((value) => {
        statValues[index] = value;
        statValues = [...statValues];
      })
    );

    stats.forEach((stat, index) => statStores[index].set(stat.target));

    return () => {
      clearInterval(id);
      statUnsubs.forEach((unsub) => unsub());
    };
  });
</script>

<div
  class="page"
  style={`--accent: ${themeChoice.accent}; --accent-2: ${themeChoice.accentTwo}; --beam: ${themeChoice.beam}; --signal: ${$signalPower}; --hue: ${hueShift}deg; --tilt: ${tilt}deg;`}
>
  <div class="nav-overlay" class:open={menuOpen} on:click={closeMenu} role="presentation"></div>
  <header class="site-header">
    <div class="logo" aria-label="Coskun">
      <span class="logo-main">Coskun</span>
      <span class="logo-sub">Googie Personal Studio</span>
      <span class="logo-stamp">Est. 1961</span>
    </div>
    <nav class="nav" class:open={menuOpen}>
      <a href="#work" on:click={closeMenu}>Work</a>
      <a href="#experiments" on:click={closeMenu}>Experiments</a>
      <a href="#studio" on:click={closeMenu}>Studio</a>
      <a href="#timeline" on:click={closeMenu}>Timeline</a>
      <a href="#now" on:click={closeMenu}>Now</a>
      <a href="#contact" on:click={closeMenu}>Contact</a>
    </nav>
    <a class="cta small header-cta" href="#contact">Signal Me</a>
    <button class="menu-toggle" class:open={menuOpen} on:click={toggleMenu} aria-label="Toggle menu" type="button">
      <span></span>
    </button>
  </header>

  <main>
    <section class="hero" id="home">
      <div class="hero-copy">
        <p class="eyebrow">Designer, builder, and collector of real-world cues</p>
        <h1>Coskun builds playful interfaces inspired by the streets, not templates.</h1>
        <p class="lead">
          The internet does not have to look one way. This personal studio pulls from Googie
          signage, travel ephemera, and bold geometry to prove websites can be physical, bright,
          and still modern.
        </p>
        <div class="hero-actions">
          <a class="cta primary" href="#work">See the Work</a>
          <a class="cta ghost" href="#contact">Say Hello</a>
        </div>
        <div class="hero-stats">
          {#each stats as stat, index}
            <div>
              <span class="stat-number">{Math.round(statValues[index])}{stat.suffix}</span>
              <span class="stat-label">{stat.label}</span>
            </div>
          {/each}
        </div>
      </div>
      <div class="signal-console" aria-hidden="true">
        <div class="console-visual">
          <svg class="console-svg" viewBox="0 0 480 420" role="presentation" aria-hidden="true">
            <defs>
              <linearGradient id="boomA" x1="0" y1="0" x2="1" y2="1">
                <stop offset="0%" stop-color="var(--accent)" />
                <stop offset="100%" stop-color="var(--sky)" />
              </linearGradient>
              <linearGradient id="boomB" x1="0" y1="0" x2="1" y2="1">
                <stop offset="0%" stop-color="var(--accent-2)" />
                <stop offset="100%" stop-color="var(--beam)" />
              </linearGradient>
            </defs>
            <path class="signal" in:draw={{ duration: 1400 }} d="M70 110 C200 20 300 20 430 90" />
            <path class="signal thin" in:draw={{ duration: 1600 }} d="M90 140 C210 70 300 70 410 120" />
            <path
              class="starburst"
              in:draw={{ duration: 1200 }}
              d="M240 40 L254 70 L288 60 L272 92 L306 100 L272 112 L288 144 L254 132 L240 166 L226 132 L192 144 L208 112 L174 100 L208 92 L192 60 L226 70 Z"
            />
            <path class="boom" d="M60 250 C160 120 320 120 420 210" />
            <path class="boom alt" d="M80 295 C180 220 300 220 400 260" />
            <polygon class="runway" points="200 260 300 260 340 390 160 390" />
            <line class="runway-line" x1="250" y1="275" x2="250" y2="380" />
            <line class="runway-line short" x1="230" y1="290" x2="230" y2="340" />
            <rect class="pylon" x="318" y="140" width="46" height="170" rx="18" />
            <rect class="sign-panel" x="276" y="100" width="130" height="56" rx="18" />
            <rect class="sign-window" x="296" y="118" width="90" height="18" rx="9" />
            <circle class="beacon glow" cx="130" cy="360" r="30" />
            <circle class="beacon" cx="130" cy="360" r="16" />
          </svg>
          <div class="console-tag">Runway Lab</div>
        </div>
        <div class="console-panel">
          <div class="panel-top">
            <span>Signal Board</span>
            <span class="panel-mode">{themeChoice.name}</span>
          </div>
          <div class="panel-screen">
            {#key boardMessage}
              <div class="panel-message" in:fly={{ y: 10, duration: 220 }} out:fade>
                {boardMessage}
              </div>
            {/key}
          </div>
          <div class="panel-meters">
            <div class="meter">
              <span>Power</span>
              <div class="meter-track">
                <span class="meter-fill" style={`width: ${$signalPower}%`}></span>
              </div>
              <span class="meter-value">{Math.round($signalPower)}%</span>
            </div>
            <div class="meter">
              <span>Hue</span>
              <div class="meter-track">
                <span class="meter-fill alt" style={`width: ${huePercent}%`}></span>
              </div>
              <span class="meter-value">{huePercent}%</span>
            </div>
            <div class="meter">
              <span>Tilt</span>
              <div class="meter-track">
                <span class="meter-fill warm" style={`width: ${tiltPercent}%`}></span>
              </div>
              <span class="meter-value">{tiltPercent}%</span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section class="manifesto" id="manifesto">
      <div class="section-head">
        <h2>Googie DNA</h2>
        <p>A reminder that the web can feel like a place, not just a layout.</p>
      </div>
      <div class="manifesto-grid">
        {#each principles as item, index}
          <article class="manifesto-card" style={`--delay: ${index * 120}ms`}>
            <h3>{item.title}</h3>
            <p>{item.copy}</p>
            <span class="tag">{item.tag}</span>
          </article>
        {/each}
      </div>
    </section>

    <section class="signal-strip" aria-label="Coskun signal">
      <div class="strip-track">
        <span>Websites can be physical</span>
        <span>Neon is a navigation tool</span>
        <span>Geometry beats grids</span>
        <span>Design from the street</span>
        <span>Motion shows the way</span>
        <span>Websites can be physical</span>
      </div>
    </section>

    <section class="mixer" id="studio">
      <div class="section-head">
        <h2>Signal mixer</h2>
        <p>Live controls to prove that interfaces can feel engineered and playful.</p>
      </div>
      <div class="mixer-grid">
        <div class="mixer-controls">
          <label>
            Signal power
            <input type="range" min="30" max="100" bind:value={powerControl} />
          </label>
          <label>
            Hue shift
            <input type="range" min="-30" max="30" bind:value={hueShift} />
          </label>
          <label>
            Sign tilt
            <input type="range" min="-15" max="15" bind:value={tilt} />
          </label>
          <div class="theme-row">
            {#each themes as theme}
              <button
                class:active={themeChoice.name === theme.name}
                on:click={() => (themeChoice = theme)}
                type="button"
              >
                {theme.name}
              </button>
            {/each}
          </div>
        </div>
        <div class="mixer-display" style="filter: hue-rotate(var(--hue));">
          <div class="display-sign">
            <span>Coskun Signal</span>
          </div>
          <div class="display-beam"></div>
          <div class="display-badge">Online</div>
          <div class="display-grid">
            <div class="display-node"></div>
            <div class="display-node"></div>
            <div class="display-node"></div>
            <div class="display-node"></div>
          </div>
        </div>
      </div>
    </section>

    <section class="work" id="work">
      <div class="section-head">
        <h2>Selected work</h2>
        <p>Product and identity systems that borrow from signage, travel, and architecture.</p>
      </div>
      <div class="work-controls">
        <div class="filter-row">
          {#each filters as filter}
            <button
              class:active={activeFilter === filter}
              on:click={() => (activeFilter = filter)}
              type="button"
            >
              {filter}
            </button>
          {/each}
        </div>
        <div class="sort-row">
          {#each sortModes as mode}
            <button class:active={sortMode === mode} on:click={() => (sortMode = mode)} type="button">
              {mode}
            </button>
          {/each}
        </div>
      </div>
      <div class="work-grid">
        {#each sortedProjects as project (project.name)}
          <article
            class="work-card"
            transition:scale={{ duration: 220 }}
            animate:flip
            style={`--delay: ${project.year - 2019}ms`}
          >
            <div class="work-header">
              <h3>{project.name}</h3>
              <span class="work-role">{project.role}</span>
            </div>
            <p>{project.desc}</p>
            <div class="work-meta">
              <span>{project.type}</span>
              <span>{project.year}</span>
            </div>
            <div class="work-tags">
              {#each project.tags as tag}
                <span>{tag}</span>
              {/each}
            </div>
          </article>
        {/each}
      </div>
    </section>

    <section class="experiments" id="experiments">
      <div class="section-head">
        <h2>Experiments and play</h2>
        <p>Small explorations that keep the Googie toolkit alive.</p>
      </div>
      <div class="experiment-grid">
        {#each experiments as experiment}
          <article
            class={`experiment-card ${openExperiment === experiment.title ? 'open' : ''}`}
            on:click={() =>
              (openExperiment = openExperiment === experiment.title ? '' : experiment.title)}
            role="button"
            tabindex="0"
            on:keydown={(event) => event.key === 'Enter' && (openExperiment = experiment.title)}
          >
            <span class="experiment-format">{experiment.format}</span>
            <h3>{experiment.title}</h3>
            <p>{experiment.desc}</p>
            {#if openExperiment === experiment.title}
              <p class="experiment-detail" transition:fade>{experiment.detail}</p>
            {/if}
          </article>
        {/each}
      </div>
    </section>

    <section class="studio" aria-label="Studio process">
      <div class="section-head">
        <h2>Studio process</h2>
        <p>From roadside cues to on-screen systems.</p>
      </div>
      <div class="studio-board">
        {#each studioSteps as step, index}
          <article class="studio-step" in:fly={{ y: 16, duration: 240 }} style={`--delay: ${index * 120}ms`}>
            <h3>{step.title}</h3>
            <p>{step.desc}</p>
          </article>
        {/each}
      </div>
    </section>

    <section class="timeline" id="timeline">
      <div class="section-head">
        <h2>Timeline</h2>
        <p>A short path through the work so far.</p>
      </div>
      <div class="timeline-list">
        {#each timeline as entry, index}
          <article class="timeline-item" style={`--delay: ${index * 120}ms`}>
            <span class="timeline-year">{entry.year}</span>
            <div>
              <h3>{entry.title}</h3>
              <p>{entry.detail}</p>
            </div>
          </article>
        {/each}
      </div>
    </section>

    <section class="now" id="now">
      <div class="now-card">
        <div>
          <h2>Now</h2>
          <p>Where the studio is focused right now.</p>
        </div>
        <ul>
          {#each nowItems as item}
            <li>{item}</li>
          {/each}
        </ul>
      </div>
    </section>

    <section class="contact" id="contact">
      <div class="contact-card">
        <div>
          <h2>Send a signal</h2>
          <p>Open for collaborations that want bold, real-world inspired interfaces.</p>
          <div class="contact-links">
            {#each links as link}
              <div>
                <span>{link.label}</span>
                <p>{link.value}</p>
              </div>
            {/each}
          </div>
        </div>
        <form class="contact-form" on:submit|preventDefault={noop}>
          <label>
            Project name
            <input type="text" name="project" placeholder="Skyline Portal" required />
          </label>
          <label>
            What do you need
            <textarea name="details" rows="3" placeholder="A Googie-inspired web experience"></textarea>
          </label>
          <button class="cta primary" type="submit">Send Inquiry</button>
        </form>
      </div>
    </section>
  </main>

  <footer class="site-footer">
    <p>Coskun Studio. Googie energy, real-world inspiration, playful outcomes.</p>
    <div class="footer-links">
      <a href="#work">Work</a>
      <a href="#experiments">Experiments</a>
      <a href="#studio">Studio</a>
      <a href="#contact">Contact</a>
    </div>
  </footer>
</div>
