<script>
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
      tags: ['Web', 'Mapping']
    },
    {
      name: 'Orbit Planner',
      role: 'Interaction design',
      desc: 'A scheduling tool for studios that treats time like a runway.',
      tags: ['Systems', 'SaaS']
    },
    {
      name: 'Neon Specimen',
      role: 'Visual system',
      desc: 'A type exploration that mixes signage, tickets, and hand-lettering.',
      tags: ['Identity', 'Type']
    },
    {
      name: 'Drive-In Toolkit',
      role: 'Creative code',
      desc: 'Reusable motion patterns inspired by roadside signage and travel boards.',
      tags: ['Motion', 'UI']
    }
  ];

  const experiments = [
    {
      title: 'Starburst Generator',
      format: 'SVG tool',
      desc: 'Builds retro bursts with adjustable rays and glow layers.'
    },
    {
      title: 'Ticket Stub UI',
      format: 'Component study',
      desc: 'Explores clipped corners, embossing, and ink-stamp textures.'
    },
    {
      title: 'Runway Lightline',
      format: 'Motion loop',
      desc: 'A looping guide rail animation for navigation cues.'
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

  const noop = () => {};
</script>

<div class="page">
  <header class="site-header">
    <div class="logo" aria-label="Coskun">
      <span class="logo-main">Coskun</span>
      <span class="logo-sub">Googie Personal Studio</span>
      <span class="logo-stamp">Est. 1961</span>
    </div>
    <nav class="nav">
      <a href="#work">Work</a>
      <a href="#experiments">Experiments</a>
      <a href="#studio">Studio</a>
      <a href="#timeline">Timeline</a>
      <a href="#now">Now</a>
      <a href="#contact">Contact</a>
    </nav>
    <a class="cta small" href="#contact">Signal Me</a>
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
          <div>
            <span class="stat-number">15+</span>
            <span class="stat-label">Visual Systems</span>
          </div>
          <div>
            <span class="stat-number">8</span>
            <span class="stat-label">Motion Toolkits</span>
          </div>
          <div>
            <span class="stat-number">24</span>
            <span class="stat-label">City Drives</span>
          </div>
        </div>
      </div>
      <div class="hero-collage" aria-hidden="true">
        <svg class="collage" viewBox="0 0 520 520" role="presentation" aria-hidden="true">
          <defs>
            <linearGradient id="boomA" x1="0" y1="0" x2="1" y2="1">
              <stop offset="0%" stop-color="#39d0c3" />
              <stop offset="100%" stop-color="#c6f2ff" />
            </linearGradient>
            <linearGradient id="boomB" x1="0" y1="0" x2="1" y2="1">
              <stop offset="0%" stop-color="#ff7b57" />
              <stop offset="100%" stop-color="#ffc857" />
            </linearGradient>
          </defs>
          <path class="boom" d="M70 300 C150 190 330 170 440 220 C470 238 476 265 458 285 C420 335 260 350 160 330 C110 320 80 310 70 300 Z" />
          <path class="boom alt" d="M90 360 C160 290 300 280 400 310 C430 320 430 350 400 370 C330 410 210 410 120 390 C90 380 80 370 90 360 Z" />
          <polygon class="roof" points="140 230 340 220 300 170 110 180" />
          <rect class="tower" x="350" y="90" width="60" height="180" rx="16" />
          <rect class="tower-panel" x="332" y="70" width="96" height="52" rx="14" />
          <polygon class="starburst" points="260,60 272,90 302,78 290,106 320,110 290,124 302,152 272,140 260,170 248,140 218,152 230,124 200,110 230,106 218,78 248,90" />
          <path class="signal" d="M90 120 C200 40 320 40 430 110" />
          <path class="signal thin" d="M100 150 C210 90 310 90 420 140" />
          <rect class="runway" x="180" y="250" width="160" height="200" rx="20" />
          <line class="runway-line" x1="260" y1="270" x2="260" y2="430" />
          <line class="runway-line short" x1="240" y1="290" x2="240" y2="360" />
          <circle class="beacon" cx="130" cy="420" r="20" />
          <circle class="beacon glow" cx="130" cy="420" r="36" />
        </svg>
        <div class="hero-sticker">Signal: Online</div>
        <div class="hero-ticket">
          <p class="ticket-title">Coskun Pass</p>
          <p class="ticket-code">GOOG-1961</p>
          <p class="ticket-copy">UI systems + motion studies</p>
          <span class="ticket-price">Open 2025</span>
        </div>
      </div>
    </section>

    <section class="manifesto" id="manifesto">
      <div class="section-head">
        <h2>Why Googie, why now</h2>
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

    <section class="work" id="work">
      <div class="section-head">
        <h2>Selected work</h2>
        <p>Product and identity systems that borrow from signage, travel, and architecture.</p>
      </div>
      <div class="work-grid">
        {#each projects as project, index}
          <article class="work-card" style={`--delay: ${index * 110}ms`}>
            <div class="work-header">
              <h3>{project.name}</h3>
              <span class="work-role">{project.role}</span>
            </div>
            <p>{project.desc}</p>
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
        {#each experiments as experiment, index}
          <article class="experiment-card" style={`--delay: ${index * 120}ms`}>
            <span class="experiment-format">{experiment.format}</span>
            <h3>{experiment.title}</h3>
            <p>{experiment.desc}</p>
          </article>
        {/each}
      </div>
    </section>

    <section class="studio" id="studio">
      <div class="section-head">
        <h2>Studio process</h2>
        <p>From roadside cues to on-screen systems.</p>
      </div>
      <div class="studio-board">
        {#each studioSteps as step, index}
          <article class="studio-step" style={`--delay: ${index * 140}ms`}>
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
