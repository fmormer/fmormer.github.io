---
layout: default
title: "Morie Software Platform"
permalink: /software/
description: "Purpose-built software modules for floating offshore wind engineering — from seabed to turbine."
og_title: "Morie Software Platform — Floating Wind Engineering"
og_description: "Purpose-built tools for site definition, anchor design, and the full floating wind engineering workflow — from bathymetry to cable layout."
og_image: "/img/posts/morie_site/morie_site.png"
og_type: "website"
---

<!-- ── HERO ─────────────────────────────────────────────────────────── -->
<section class="hero plat-hero" aria-label="Morie Software Platform hero">
  <div class="hero-background">
    <img src="{{ '/img/posts/morie_site/morie_site.png' | relative_url }}"
         alt="Offshore floating wind farm site definition — Morie Software Platform">
  </div>
  <div class="hero-overlay plat-hero__overlay"></div>
  <div class="hero-inner">
    <div class="hero-callout">
      <div class="hero-left">
        <h1 class="hero-title">
          One platform for floating wind<br>
          <span>engineering, from seabed to turbine</span>
        </h1>
        <p class="hero-subtitle">
          Stop hunting data across disconnected tools. Morie Platform combines environmental datasets,
          geotechnical profiles, and engineering calculations in a single collaborative workspace —
          so your team spends less time collating data and more time iterating designs.
        </p>
        <p class="hero-tagline">Built by offshore wind engineers, for offshore wind engineers.</p>
        <div class="hero-buttons">
          <a href="#request-access" class="hero-button hero-button--secondary">Request Access</a>
          <a href="#live-tools" class="hero-button hero-button--primary">See the Tools</a>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ── LIVE TOOLS ────────────────────────────────────────────────────── -->
<section class="plat-tools" id="live-tools" aria-label="Live tools — Site and Anchor">
  <div class="plat-container">
    <p class="home-storyband__eyebrow">Live today</p>
    <h2 class="plat-section__title">Two powerful tools available now</h2>

    <article class="plat-tool-card" aria-labelledby="tool-site-heading">
      <div class="plat-tool-card__media">
        <img src="{{ '/img/posts/morie_site/celtic_sea_lease_areas.png' | relative_url }}"
             alt="Morie Site Tool — Celtic Sea lease area boundary definition on interactive map"
             loading="lazy">
      </div>
      <div class="plat-tool-card__body">
        <span class="plat-tool-card__badge">Site Tool</span>
        <h3 id="tool-site-heading" class="plat-tool-card__title">
          From blank map to full site dataset — in minutes
        </h3>
        <p class="plat-tool-card__lead">
          Draw your site polygon on an interactive map and let the platform do the heavy lifting.
          No data downloads. No manual preprocessing. The Site Tool automatically extracts and
          harmonises the environmental data your workflow depends on.
        </p>
        <ul class="plat-feature-list" aria-label="Site Tool features">
          <li><i class="ion ion-md-checkmark-circle" aria-hidden="true"></i> Interactive polygon drawing for project boundary definition</li>
          <li><i class="ion ion-md-checkmark-circle" aria-hidden="true"></i> Automatic bathymetry extraction at configurable grid resolution (10–200 cells)</li>
          <li><i class="ion ion-md-checkmark-circle" aria-hidden="true"></i> Environmental data pull from validated public marine sources</li>
          <li><i class="ion ion-md-checkmark-circle" aria-hidden="true"></i> Named studies per project — iterate without losing previous runs</li>
        </ul>
      </div>
    </article>

    <article class="plat-tool-card plat-tool-card--reverse" aria-labelledby="tool-anchor-heading">
      <div class="plat-tool-card__media">
        <img src="{{ '/img/posts/morie_anchor/anchor_types.png' | relative_url }}"
             alt="Morie Anchor Tool — nine anchor types supported including suction pile, plate DEA, SEPLA, torpedo and driven pile"
             loading="lazy">
      </div>
      <div class="plat-tool-card__body">
        <span class="plat-tool-card__badge">Anchor Tool</span>
        <h3 id="tool-anchor-heading" class="plat-tool-card__title">
          Nine anchor types. Any soil profile. Real-time 3D geometry.
        </h3>
        <p class="plat-tool-card__lead">
          Configure any anchor type, build a multi-layer soil profile, and get factor-of-safety results —
          all within your project workspace. The 3D viewer updates in real time as you adjust geometry inputs,
          so you see the design change before you run the analysis.
        </p>
        <ul class="plat-feature-list" aria-label="Anchor Tool features">
          <li><i class="ion ion-md-checkmark-circle" aria-hidden="true"></i> 9 anchor types: suction pile, plate DEA, SEPLA, DEPLA, VLA, torpedo, helical, driven, drilled</li>
          <li><i class="ion ion-md-checkmark-circle" aria-hidden="true"></i> Multi-layer soil profile builder — clay, sand, and rock</li>
          <li><i class="ion ion-md-checkmark-circle" aria-hidden="true"></i> 3D anchor geometry viewer that updates in real time</li>
          <li><i class="ion ion-md-checkmark-circle" aria-hidden="true"></i> Horizontal and vertical load input with factor-of-safety acceptance criteria</li>
          <li><i class="ion ion-md-checkmark-circle" aria-hidden="true"></i> Multiple studies per project for parametric design iteration</li>
        </ul>
      </div>
    </article>
  </div>
</section>

<!-- ── COMING SOON ───────────────────────────────────────────────────── -->
<section class="plat-soon" aria-label="Tools in development">
  <div class="plat-container">
    <p class="home-storyband__eyebrow">In development</p>
    <h2 class="plat-section__title">Five more tools on the way</h2>
    <p class="plat-section__lead">
      The full engineering pipeline is being built module by module. Here's what's coming next.
    </p>
    <div class="plat-soon__grid">

      <div class="plat-soon__item">
        <div class="plat-soon__icon">
          <img src="{{ '/img/morie_icon_layout.png' | relative_url }}" alt="">
        </div>
        <h3>Layout</h3>
        <p>Optimised turbine placement within site constraints and environmental loading.</p>
      </div>

      <div class="plat-soon__item">
        <div class="plat-soon__icon">
          <img src="{{ '/img/morie_icon_subsurface.png' | relative_url }}" alt="">
        </div>
        <h3>Soil</h3>
        <p>Multi-layer geotechnical model builder and spatial interpolation across the farm footprint.</p>
      </div>

      <div class="plat-soon__item">
        <div class="plat-soon__icon">
          <img src="{{ '/img/morie_icon_mooring.png' | relative_url }}" alt="">
        </div>
        <h3>Mooring</h3>
        <p>Catenary and taut-leg mooring analysis with shared-anchor configurations.</p>
      </div>

      <div class="plat-soon__item">
        <div class="plat-soon__icon">
          <img src="{{ '/img/morie_icon_cable.png' | relative_url }}" alt="">
        </div>
        <h3>Cable</h3>
        <p>Inter-array and export cable routing and sizing.</p>
      </div>

      <div class="plat-soon__item">
        <div class="plat-soon__icon">
          <img src="{{ '/img/morie_icon_atlas.png' | relative_url }}" alt="">
        </div>
        <h3>Atlas</h3>
        <p>Integrated project atlas — full-farm anchor mapping, cost estimation and comparison views.</p>
      </div>

    </div>
  </div>
</section>

<!-- ── COLLABORATION ─────────────────────────────────────────────────── -->
<section class="plat-collab" aria-label="Collaboration and team features">
  <div class="plat-container">
    <p class="home-storyband__eyebrow">Built for teams</p>
    <h2 class="plat-section__title">Work together, not in parallel</h2>
    <p class="plat-section__lead">
      Morie Platform is organised around projects. Each project holds multiple studies per tool,
      so your team can run design iterations without overwriting each other's work.
    </p>
    <div class="plat-collab__grid">
      <div class="plat-collab__item">
        <i class="ion ion-md-folder-open plat-collab__icon" aria-hidden="true"></i>
        <h3>Project workspaces</h3>
        <p>Group all tools and studies under a single project. Share context across Site, Anchor, and future tools without re-entering data.</p>
      </div>
      <div class="plat-collab__item">
        <i class="ion ion-md-key plat-collab__icon" aria-hidden="true"></i>
        <h3>Role-based access</h3>
        <p>Assign <strong>Viewer</strong>, <strong>Editor</strong>, or <strong>Owner</strong> roles per project. Keep sensitive studies locked down while sharing results freely.</p>
      </div>
      <div class="plat-collab__item">
        <i class="ion ion-md-business plat-collab__icon" aria-hidden="true"></i>
        <h3>Organisation plans</h3>
        <p>Manage your whole team under one organisation account. Custom subdomains (<code>yourorg.morie.io</code>) keep your workspace identifiable.</p>
      </div>
      <div class="plat-collab__item">
        <i class="ion ion-md-copy plat-collab__icon" aria-hidden="true"></i>
        <h3>Multiple studies per tool</h3>
        <p>Run parametric variants within the same project. Compare results across design iterations without duplicating setup work.</p>
      </div>
    </div>
  </div>
</section>

<!-- ── REQUEST ACCESS ────────────────────────────────────────────────── -->
<section class="plat-access" id="request-access" aria-label="Request early access to Morie Platform">
  <div class="plat-container">
    <div class="plat-access__header">
      <p class="home-storyband__eyebrow">Early access</p>
      <h2 class="plat-section__title plat-section__title--light">
        Join the engineers shaping floating wind
      </h2>
      <p class="plat-access__lead">
        Morie Platform is available by invitation only. We are working with a select group of
        offshore wind engineers, consultancies, developers and classification societies to
        refine the tools before broader release.
      </p>
    </div>
    <div class="plat-access__body">
      <div class="plat-access__features">
        <ul class="plat-feature-list plat-feature-list--light" aria-label="What early access includes">
          <li><i class="ion ion-md-checkmark-circle" aria-hidden="true"></i> Site Tool — interactive boundary definition and bathymetry extraction</li>
          <li><i class="ion ion-md-checkmark-circle" aria-hidden="true"></i> Anchor Tool — 9 anchor types, multi-layer soil profiles, 3D geometry viewer</li>
          <li><i class="ion ion-md-checkmark-circle" aria-hidden="true"></i> New tools as they are released (Layout, Soil, Mooring, Cable, Atlas)</li>
          <li><i class="ion ion-md-checkmark-circle" aria-hidden="true"></i> Project workspaces with multiple studies per tool</li>
          <li><i class="ion ion-md-checkmark-circle" aria-hidden="true"></i> Role-based access — Viewer, Editor, and Owner</li>
          <li><i class="ion ion-md-checkmark-circle" aria-hidden="true"></i> Organisation account with custom subdomain</li>
          <li><i class="ion ion-md-checkmark-circle" aria-hidden="true"></i> Direct support from the Morie Analytics team</li>
        </ul>
      </div>
      <div class="plat-access__form-wrap">
        <form class="plat-access__form"
              action="https://formspree.io/f/xgodwlar"
              method="POST"
              aria-label="Request early access form">
          <div class="plat-form__group">
            <label class="plat-form__label" for="access-name">Name</label>
            <input class="plat-form__input" type="text" id="access-name" name="name"
                   autocomplete="name" required placeholder="Your full name">
          </div>
          <div class="plat-form__group">
            <label class="plat-form__label" for="access-email">Work email</label>
            <input class="plat-form__input" type="email" id="access-email" name="email"
                   autocomplete="email" required placeholder="you@yourorg.com">
          </div>
          <div class="plat-form__group">
            <label class="plat-form__label" for="access-org">Organisation</label>
            <input class="plat-form__input" type="text" id="access-org" name="organisation"
                   autocomplete="organization" placeholder="Consulting firm, developer, society…">
          </div>
          <div class="plat-form__group">
            <label class="plat-form__label" for="access-context">Project context</label>
            <textarea class="plat-form__input plat-form__textarea" id="access-context"
                      name="context" rows="4"
                      placeholder="Briefly describe your floating wind project and how you would use Morie Platform."></textarea>
          </div>
          <button class="plat-form__submit" type="submit">
            Request early access
          </button>
          <p class="plat-form__note">We respond within 2–3 business days. No marketing emails.</p>
        </form>
      </div>
    </div>
  </div>
</section>

<!-- ── JSON-LD Structured Data ───────────────────────────────────────── -->
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "SoftwareApplication",
  "name": "Morie Platform",
  "applicationCategory": "EngineeringApplication",
  "operatingSystem": "Web",
  "description": "SaaS platform for offshore floating wind engineering. Integrates environmental data, geotechnical profiles, and engineering calculations into a collaborative workspace.",
  "offers": [
    { "@type": "Offer", "name": "Free", "price": "0", "priceCurrency": "USD" },
    { "@type": "Offer", "name": "Starter" },
    { "@type": "Offer", "name": "Pro" },
    { "@type": "Offer", "name": "Enterprise" }
  ],
  "featureList": [
    "Interactive site boundary definition with bathymetry extraction",
    "9 anchor types with multi-layer soil profile builder",
    "3D real-time anchor geometry viewer",
    "Project-based collaborative workspaces",
    "Role-based access control (viewer, editor, owner)",
    "Organisation plans with custom subdomains"
  ],
  "provider": {
    "@type": "Organization",
    "name": "Morie Analytics",
    "url": "https://morie.io"
  }
}
</script>

<!-- Smooth scroll with nav offset -->
<script>
  document.querySelectorAll('a[href^="#"]').forEach(function(anchor) {
    anchor.addEventListener('click', function(e) {
      var target = document.querySelector(this.getAttribute('href'));
      if (!target) return;
      e.preventDefault();
      var top = target.getBoundingClientRect().top + window.pageYOffset - 56;
      window.scrollTo({ top: top, behavior: 'smooth' });
    });
  });
</script>
