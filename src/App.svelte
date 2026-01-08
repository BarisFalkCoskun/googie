<script>
  const highlights = [
    {
      title: 'Jet-Stream Launch Pad',
      copy: 'A vaulted arrival canopy with kinetic light pylons and a sweeping, runway-ready deck.',
      note: 'Open daily'
    },
    {
      title: 'Neon Signal Bar',
      copy: 'Interactive consoles that paint the room with analog dials, color wheels, and pulse meters.',
      note: 'Hands-on'
    },
    {
      title: 'Signal Studio',
      copy: 'A listening lounge with vinyl capsules, jukebox benches, and moonlit acoustics.',
      note: 'Live sets'
    }
  ];

  const programs = [
    {
      name: 'Orbit Capsule Exhibit',
      desc: 'Immersive kinetic sculpture pods with projected mid-century futures.',
      price: '$14'
    },
    {
      name: 'Skyline Model Lab',
      desc: 'Hands-on model kits, laser-cut parts, and pinstripe paint bays.',
      price: '$12'
    },
    {
      name: 'Sunset Projection Room',
      desc: 'Short films on Googie architects, neon signage, and concept cars.',
      price: '$10'
    },
    {
      name: 'Signal Workshop',
      desc: 'Weekend sessions on type, signage, and retro-future illustration.',
      price: '$18'
    }
  ];

  const events = [
    {
      title: 'Starliner Swing',
      time: 'Friday 8:00 PM',
      detail: 'Big-band sets with a chrome-lit dance floor.'
    },
    {
      title: 'Midnight Motors',
      time: 'Saturday 10:30 PM',
      detail: 'Retro auto cinema with popcorn flight service.'
    },
    {
      title: 'Coskun Radio',
      time: 'Sunday 6:00 PM',
      detail: 'Live broadcast from the signal booth.'
    }
  ];

  const locations = [
    {
      name: 'Coskun Retro Plaza',
      address: '88 Skyline Spur, Crescent Bay, CA',
      hours: 'Daily 7 AM - 1 AM'
    },
    {
      name: 'Coskun Airfield',
      address: '212 Jetstream Ave, Palm Mesa, AZ',
      hours: 'Thu-Sun 8 AM - Late'
    }
  ];

  const noop = () => {};
</script>

<div class="page">
  <header class="site-header">
    <div class="logo-burst" aria-label="Coskun">
      <span class="logo-word">Coskun</span>
      <span class="logo-tag">Googie Design House</span>
    </div>
    <nav class="nav">
      <a href="#story">Story</a>
      <a href="#programs">Programs</a>
      <a href="#events">Events</a>
      <a href="#visit">Visit</a>
      <button class="cta small">Plan Visit</button>
    </nav>
  </header>

  <main>
    <section class="hero" id="story">
      <div class="hero-copy">
        <p class="kicker">Googie drive-in gallery + design lab</p>
        <h1>Coskun is where the chrome future met the open road.</h1>
        <p class="lead">
          Bold forms, boomerang architecture, and a soundtrack of neon nights. Pull into a bay
          under the starburst canopy and explore the retro-future.
        </p>
        <div class="hero-actions">
          <button class="cta primary">Reserve a Bay</button>
          <button class="cta ghost">Tonight's Program</button>
        </div>
        <div class="hero-metrics">
          <div>
            <span class="metric-number">12</span>
            <span class="metric-label">Neon Bays</span>
          </div>
          <div>
            <span class="metric-number">60s</span>
            <span class="metric-label">Vinyl Capsules</span>
          </div>
          <div>
            <span class="metric-number">24</span>
            <span class="metric-label">Retro Builds</span>
          </div>
        </div>
      </div>
      <div class="hero-art" aria-hidden="true">
        <div class="boomerang"></div>
        <div class="boomerang alt"></div>
        <div class="starburst">Open Late</div>
        <div class="orbit-card">
          <p class="orbit-title">Skyline Pass</p>
          <p class="orbit-copy">3-exhibit loop + glow kit</p>
          <span class="orbit-price">$28</span>
        </div>
        <div class="signal-lines"></div>
      </div>
    </section>

    <section class="highlights" id="highlights">
      <div class="section-head">
        <h2>Attractions in orbit</h2>
        <p>Vintage glamour meets playful geometry, all tuned for a cosmic pit stop.</p>
      </div>
      <div class="cards">
        {#each highlights as highlight, index}
          <article class="card" style={`--delay: ${index * 140}ms`}>
            <h3>{highlight.title}</h3>
            <p>{highlight.copy}</p>
            <span class="chip">{highlight.note}</span>
          </article>
        {/each}
      </div>
    </section>

    <section class="programs" id="programs">
      <div class="section-head">
        <h2>Coskun program board</h2>
        <p>Immersive exhibits and hands-on sessions, tuned for the open highway.</p>
      </div>
      <div class="program-board">
        {#each programs as item}
          <div class="program-item">
            <div>
              <h3>{item.name}</h3>
              <p>{item.desc}</p>
            </div>
            <span class="price">{item.price}</span>
          </div>
        {/each}
      </div>
    </section>

    <section class="marquee" aria-label="Coskun vibe">
      <div class="marquee-track">
        <span>Neon nights</span>
        <span>Chrome concepts</span>
        <span>Rocket rhythms</span>
        <span>Jet-lagged sketches</span>
        <span>Drive-in glow</span>
        <span>Neon nights</span>
        <span>Chrome concepts</span>
        <span>Rocket rhythms</span>
      </div>
    </section>

    <section class="split" id="events">
      <div class="events">
        <div class="section-head">
          <h2>Tonight on the signal</h2>
          <p>Live acts, late-night films, and dance-floor flare every week.</p>
        </div>
        <div class="events-list">
          {#each events as event, index}
            <div class="event" style={`--delay: ${index * 150}ms`}>
              <h3>{event.title}</h3>
              <p class="event-time">{event.time}</p>
              <p>{event.detail}</p>
            </div>
          {/each}
        </div>
      </div>
      <div class="visit" id="visit">
        <div class="section-head">
          <h2>Visit the runway</h2>
          <p>Two glow-lit hangars, both with plenty of stargazer parking.</p>
        </div>
        <div class="locations">
          {#each locations as location}
            <div class="location">
              <h3>{location.name}</h3>
              <p>{location.address}</p>
              <span class="chip">{location.hours}</span>
            </div>
          {/each}
        </div>
        <button class="cta primary">Get Directions</button>
      </div>
    </section>

    <section class="newsletter">
      <div>
        <h2>Coskun Dispatch</h2>
        <p>Get the weekly neon list: special programs, guest DJs, and retro ride-ins.</p>
      </div>
      <form class="newsletter-form" on:submit|preventDefault={noop}>
        <input type="email" name="email" placeholder="you@coskun.com" aria-label="Email address" required />
        <button class="cta small" type="submit">Join the Crew</button>
      </form>
    </section>
  </main>

  <footer class="site-footer">
    <p>Coskun © 1961 - 2024. Built on neon, nostalgia, and new ideas.</p>
    <div class="footer-links">
      <a href="#programs">Programs</a>
      <a href="#events">Events</a>
      <a href="#visit">Visit</a>
      <a href="#highlights">Highlights</a>
    </div>
  </footer>
</div>
