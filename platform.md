---
layout: default
title: "Morie Platform — Floating Wind Engineering SaaS"
permalink: /platform/
description: "Morie Platform is invite-only SaaS for offshore floating wind engineers. Site screening, anchor design, and the full engineering pipeline in a single collaborative workspace."
og_title: "Morie Platform — Floating Wind Engineering SaaS"
og_description: "Purpose-built tools for site definition, anchor design, and the full floating wind engineering workflow — from bathymetry to cable layout."
og_image: "/img/posts/morie_site/morie_site.png"
og_type: "website"
---

<!-- ── HERO ─────────────────────────────────────────────────────────── -->
<section class="hero plat-hero" aria-label="Morie Platform hero">
  <div class="hero-background">
    <img src="{{ '/img/posts/morie_site/morie_site.png' | relative_url }}"
         alt="Offshore floating wind farm site definition — Morie Platform">
  </div>
  <div class="hero-overlay plat-hero__overlay"></div>
  <div class="hero-inner">
    <div class="hero-callout">
      <div class="hero-left">
        <p class="plat-hero__eyebrow">Invite-only · Early Access</p>
        <h1 class="hero-title">
          One platform for floating wind<br>
          <span>engineering, from seabed to cable</span>
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

<!-- ── PROBLEM ───────────────────────────────────────────────────────── -->
<section class="plat-problem" aria-label="The problem Morie Platform solves">
  <div class="plat-container">
    <p class="home-storyband__eyebrow">The problem</p>
    <h2 class="plat-section__title">Floating wind engineering is fragmented by design</h2>
    <p class="plat-section__lead">
      Offshore floating wind projects span seven interconnected engineering disciplines — yet most teams
      work in silos, stitching together spreadsheets, GIS tools, and one-off scripts. The result is rework,
      version mismatches, and weeks lost before design even begins.
    </p>
    <div class="plat-problem__grid">
      <div class="plat-problem__item">
        <i class="ion ion-md-search plat-problem__icon" aria-hidden="true"></i>
        <h3>Data fragmentation</h3>
        <p>Bathymetry, metocean, soil, and load data live in separate systems with no shared coordinate space or version control.</p>
      </div>
      <div class="plat-problem__item">
        <i class="ion ion-md-construct plat-problem__icon" aria-hidden="true"></i>
        <h3>Manual, error-prone workflows</h3>
        <p>Copy-pasting between spreadsheets and scripts introduces silent errors that only surface late in the design cycle.</p>
      </div>
      <div class="plat-problem__item">
        <i class="ion ion-md-apps plat-problem__icon" aria-hidden="true"></i>
        <h3>No purpose-built tool</h3>
        <p>General-purpose engineering software was not built for floating offshore wind — engineers adapt tools that were never designed for this context.</p>
      </div>
      <div class="plat-problem__item">
        <i class="ion ion-md-people plat-problem__icon" aria-hidden="true"></i>
        <h3>Collaboration is an afterthought</h3>
        <p>Files shared by email, no audit trail, no role-based access — coordination overhead grows with team size.</p>
      </div>
    </div>
  </div>
</section>

<!-- ── WORKFLOW ──────────────────────────────────────────────────────── -->
<section class="plat-workflow" aria-label="Seven-step floating wind engineering workflow">
  <div class="plat-container">
    <p class="home-storyband__eyebrow">The workflow</p>
    <h2 class="plat-section__title">A connected engineering pipeline — end to end</h2>
    <p class="plat-section__lead">
      Morie Platform structures the full floating wind design chain into seven modular tools.
      Two are live today. Five are in active development.
    </p>
    <ol class="plat-pipeline" aria-label="Seven-step Morie workflow">

      <li class="plat-pipeline__step plat-pipeline__step--live" aria-label="Site Tool — Live">
        <div class="plat-pipeline__step-header">
          <span class="plat-pipeline__badge plat-pipeline__badge--live">Live</span>
          <span class="plat-pipeline__number">01</span>
        </div>
        <div class="plat-pipeline__icon">
          <img src="{{ '/img/morie_icon_site.png' | relative_url }}" alt="">
        </div>
        <h3 class="plat-pipeline__name">Site</h3>
        <p class="plat-pipeline__desc">Define project boundaries and extract bathymetry and environmental data automatically.</p>
      </li>

      <li class="plat-pipeline__step plat-pipeline__step--soon">
        <div class="plat-pipeline__step-header">
          <span class="plat-pipeline__badge plat-pipeline__badge--soon">Coming soon</span>
          <span class="plat-pipeline__number">02</span>
        </div>
        <div class="plat-pipeline__icon">
          <img src="{{ '/img/morie_icon_layout.png' | relative_url }}" alt="">
        </div>
        <h3 class="plat-pipeline__name">Layout</h3>
        <p class="plat-pipeline__desc">Optimised turbine placement within site constraints and environmental loading.</p>
      </li>

      <li class="plat-pipeline__step plat-pipeline__step--soon">
        <div class="plat-pipeline__step-header">
          <span class="plat-pipeline__badge plat-pipeline__badge--soon">Coming soon</span>
          <span class="plat-pipeline__number">03</span>
        </div>
        <div class="plat-pipeline__icon">
          <img src="{{ '/img/morie_icon_subsurface.png' | relative_url }}" alt="">
        </div>
        <h3 class="plat-pipeline__name">Soil</h3>
        <p class="plat-pipeline__desc">Multi-layer geotechnical model builder and spatial interpolation across the farm footprint.</p>
      </li>

      <li class="plat-pipeline__step plat-pipeline__step--soon">
        <div class="plat-pipeline__step-header">
          <span class="plat-pipeline__badge plat-pipeline__badge--soon">Coming soon</span>
          <span class="plat-pipeline__number">04</span>
        </div>
        <div class="plat-pipeline__icon">
          <img src="{{ '/img/morie_icon_system.png' | relative_url }}" alt="">
        </div>
        <h3 class="plat-pipeline__name">Mooring</h3>
        <p class="plat-pipeline__desc">Catenary and taut-leg mooring analysis with shared-anchor configurations.</p>
      </li>

      <li class="plat-pipeline__step plat-pipeline__step--live" aria-label="Anchor Tool — Live">
        <div class="plat-pipeline__step-header">
          <span class="plat-pipeline__badge plat-pipeline__badge--live">Live</span>
          <span class="plat-pipeline__number">05</span>
        </div>
        <div class="plat-pipeline__icon">
          <img src="{{ '/img/morie_icon_anchor.png' | relative_url }}" alt="">
        </div>
        <h3 class="plat-pipeline__name">Anchor</h3>
        <p class="plat-pipeline__desc">Nine anchor types. Multi-layer soil profiles. 3D real-time geometry viewer. Factor-of-safety design checks.</p>
      </li>

      <li class="plat-pipeline__step plat-pipeline__step--soon">
        <div class="plat-pipeline__step-header">
          <span class="plat-pipeline__badge plat-pipeline__badge--soon">Coming soon</span>
          <span class="plat-pipeline__number">06</span>
        </div>
        <div class="plat-pipeline__icon plat-pipeline__icon--placeholder" aria-hidden="true">
          <i class="ion ion-md-git-network"></i>
        </div>
        <h3 class="plat-pipeline__name">Cable</h3>
        <p class="plat-pipeline__desc">Inter-array and export cable routing and sizing.</p>
      </li>

      <li class="plat-pipeline__step plat-pipeline__step--soon">
        <div class="plat-pipeline__step-header">
          <span class="plat-pipeline__badge plat-pipeline__badge--soon">Coming soon</span>
          <span class="plat-pipeline__number">07</span>
        </div>
        <div class="plat-pipeline__icon">
          <img src="{{ '/img/morie_icon_atlas.png' | relative_url }}" alt="">
        </div>
        <h3 class="plat-pipeline__name">Atlas</h3>
        <p class="plat-pipeline__desc">Integrated project atlas — full-farm anchor mapping, cost estimation, and comparison views.</p>
      </li>

    </ol>
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
              action="{{ '/contact/' | relative_url }}"
              method="GET"
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
