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
          <svg class="console-svg" viewBox="0 0 400 360" role="presentation" aria-hidden="true">
            <defs>
              <linearGradient id="boomA" x1="0" y1="0" x2="1" y2="1">
                <stop offset="0%" stop-color="var(--accent)" />
                <stop offset="100%" stop-color="var(--sky)" />
              </linearGradient>
              <linearGradient id="boomB" x1="0" y1="0" x2="1" y2="1">
                <stop offset="0%" stop-color="var(--accent-2)" />
                <stop offset="100%" stop-color="var(--beam)" />
              </linearGradient>
              <linearGradient id="carGrad" x1="0" y1="0" x2="1" y2="0">
                <stop offset="0%" stop-color="var(--accent-2)" />
                <stop offset="50%" stop-color="var(--coral)" />
                <stop offset="100%" stop-color="var(--beam)" />
              </linearGradient>
              <linearGradient id="signGlow" x1="0" y1="0" x2="0" y2="1">
                <stop offset="0%" stop-color="var(--accent)" />
                <stop offset="100%" stop-color="var(--night)" />
              </linearGradient>
              <filter id="neonGlow" x="-50%" y="-50%" width="200%" height="200%">
                <feGaussianBlur stdDeviation="3" result="blur" />
                <feMerge>
                  <feMergeNode in="blur" />
                  <feMergeNode in="SourceGraphic" />
                </feMerge>
              </filter>
              <filter id="softGlow" x="-50%" y="-50%" width="200%" height="200%">
                <feGaussianBlur stdDeviation="8" result="blur" />
                <feMerge>
                  <feMergeNode in="blur" />
                  <feMergeNode in="SourceGraphic" />
                </feMerge>
              </filter>
            </defs>

            <!-- Googie boomerangs -->
            <path class="boom" d="M40 220 C120 120 290 110 360 160 C380 175 380 205 360 220 C270 270 120 280 55 250 C35 238 30 228 40 220 Z" />
            <path class="boom alt" d="M60 250 C140 190 250 180 320 215 C335 222 335 238 320 247 C250 275 150 290 90 270 C70 262 62 258 60 250 Z" />
            <path class="orbit" d="M70 150 C140 100 260 90 330 135" />

            <!-- Starburst -->
            <g class="starburst-group" transform="translate(210, 120)">
              <circle class="starburst-glow" cx="0" cy="0" r="52" />
              <path class="starburst-rays" d="M0 -60 L10 -18 L48 -30 L16 -8 L60 0 L16 8 L48 30 L10 18 L0 60 L-10 18 L-48 30 L-16 8 L-60 0 L-16 -8 L-48 -30 L-10 -18 Z" />
              <circle class="starburst-center" cx="0" cy="0" r="18" />
            </g>

            <!-- Googie sign tower -->
            <g class="sign-tower" transform="translate(305, 145)">
              <rect class="sign-head" x="-60" y="-22" width="120" height="44" rx="22" />
              <rect class="sign-window" x="-34" y="-8" width="68" height="16" rx="6" filter="url(#neonGlow)" />
              <rect class="sign-post" x="-12" y="22" width="24" height="110" rx="10" />
              <path class="sign-foot" d="M-28 132 L28 132 L18 150 L-18 150 Z" />
            </g>

            <!-- Runway base -->
            <path class="runway" d="M150 215 L250 215 L280 310 L120 310 Z" />
            <line class="runway-line" x1="200" y1="236" x2="200" y2="296" />
            <line class="runway-line short" x1="182" y1="246" x2="182" y2="286" />
            <line class="runway-line short" x1="218" y1="246" x2="218" y2="286" />

            <!-- Beacon -->
            <circle class="beacon-ring" cx="105" cy="292" r="18" />
            <circle class="beacon" cx="105" cy="292" r="10" />

            <!-- Decorative stars -->
            <circle class="star" cx="50" cy="50" r="3" />
            <circle class="star" cx="120" cy="30" r="2" />
            <circle class="star" cx="350" cy="45" r="2.5" />
            <circle class="star" cx="80" cy="90" r="2" />
          </svg>
          <div class="console-label">
            <span class="label-text">Signal Lab</span>
            <span class="label-dot"></span>
          </div>
        </div>
        <div class="console-panel">
          <div class="panel-header">
            <div class="panel-title">
              <span class="panel-icon"></span>
              <span>Control Deck</span>
            </div>
            <span class="panel-mode">{themeChoice.name}</span>
          </div>
          <div class="panel-screen">
            <div class="screen-scanline"></div>
            {#key boardMessage}
              <div class="panel-message" in:fly={{ y: 12, duration: 280 }} out:fade={{ duration: 150 }}>
                {boardMessage}
              </div>
            {/key}
            <div class="screen-indicator">
              {#each boardMessages as _, i}
                <span class="indicator-dot" class:active={i === boardIndex}></span>
              {/each}
            </div>
          </div>
          <div class="panel-meters">
            <div class="meter">
              <span class="meter-label">PWR</span>
              <div class="meter-track">
                <span class="meter-fill" style={`width: ${$signalPower}%`}></span>
                <span class="meter-glow" style={`width: ${$signalPower}%`}></span>
              </div>
              <span class="meter-value">{Math.round($signalPower)}</span>
            </div>
            <div class="meter">
              <span class="meter-label">HUE</span>
              <div class="meter-track">
                <span class="meter-fill alt" style={`width: ${huePercent}%`}></span>
                <span class="meter-glow alt" style={`width: ${huePercent}%`}></span>
              </div>
              <span class="meter-value">{huePercent}</span>
            </div>
            <div class="meter">
              <span class="meter-label">TLT</span>
              <div class="meter-track">
                <span class="meter-fill warm" style={`width: ${tiltPercent}%`}></span>
                <span class="meter-glow warm" style={`width: ${tiltPercent}%`}></span>
              </div>
              <span class="meter-value">{tiltPercent}</span>
            </div>
          </div>
          <div class="panel-buttons">
            {#each themes as theme}
              <button
                class="panel-btn"
                class:active={themeChoice.name === theme.name}
                on:click={() => (themeChoice = theme)}
                type="button"
                style={`--btn-color: ${theme.accent}`}
              >
                {theme.name}
              </button>
            {/each}
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
        <span>Neon is a navigation tool</span>
        <span>Geometry beats grids</span>
      </div>
      <div class="strip-border-bottom"></div>
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
          <div class="display-header">
            <span class="display-title">Signal Preview</span>
            <span class="display-status">Live</span>
          </div>
          <div class="display-main">
            <div class="display-beam"></div>
            <div class="display-decoration">
              <div class="deco-line"></div>
              <div class="deco-line"></div>
              <div class="deco-line"></div>
              <div class="deco-circle"></div>
              <div class="deco-circle"></div>
            </div>
            <div class="display-sign">
              <span>Coskun Signal</span>
            </div>
          </div>
          <div class="display-footer">
            <div class="display-meters">
              <div class="mini-meter">
                <div class="mini-meter-bar">
                  <div class="mini-meter-fill" style={`height: ${$signalPower}%`}></div>
                </div>
                <span class="mini-meter-label">Pwr</span>
              </div>
              <div class="mini-meter">
                <div class="mini-meter-bar">
                  <div class="mini-meter-fill alt" style={`height: ${huePercent}%`}></div>
                </div>
                <span class="mini-meter-label">Hue</span>
              </div>
              <div class="mini-meter">
                <div class="mini-meter-bar">
                  <div class="mini-meter-fill warm" style={`height: ${tiltPercent}%`}></div>
                </div>
                <span class="mini-meter-label">Tlt</span>
              </div>
            </div>
            <div class="display-badge">Online</div>
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
