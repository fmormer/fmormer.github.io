---
layout: default
title: "Consulting & Portfolio"
permalink: /consulting/
description: "Offshore wind and marine engineering consultancy — portfolio, capabilities and how to engage."
---

<!-- ── HERO ─────────────────────────────────────────────────────────── -->
<section class="hero plat-hero" aria-label="Consulting hero">
  <div class="hero-background">
    <img src="{{ '/img/posts/morie_site/celtic_sea_lease_areas.png' | relative_url }}"
         alt="Celtic Sea floating offshore wind lease areas">
  </div>
  <div class="hero-overlay plat-hero__overlay"></div>
  <div class="hero-inner">
    <div class="hero-callout">
      <div class="hero-left">
        <p class="plat-hero__eyebrow">Offshore Engineering Consultancy</p>
        <h1 class="hero-title">
          Offshore wind engineering consultancy<br>
          <span>from concept to design</span>
        </h1>
        <p class="hero-subtitle">
          Morie Analytics provides engineering consultancy across the full floating offshore wind design chain —
          from site characterization and layout optimization to mooring, anchor and cable engineering.
        </p>
        <p class="hero-tagline">Built on a decade of research and real-project engineering experience.</p>
        <div class="hero-buttons">
          <a href="{{ '/contact/' | relative_url }}" class="hero-button hero-button--secondary">Get in touch</a>
          <a href="#portfolio" class="hero-button hero-button--primary">View portfolio</a>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ── OFFERING ───────────────────────────────────────────────────────── -->
<section class="plat-collab" aria-label="Consulting offering">
  <div class="plat-container">
    <p class="home-storyband__eyebrow">Our offering</p>
    <h2 class="plat-section__title">Engineering consultancy across the full design chain</h2>
    <p class="plat-section__lead">
      We work across both the technical and client-facing sides of engineering: from model development,
      automation and computation to practical implementation and deployment support. Our goal is to deliver
      results that clients can adopt, extend and operate with confidence.
    </p>

    <div class="capabilities-grid">

      <div class="capability-card">
        <div class="capability-card__icon">
          <img src="{{ '/img/morie_icon_anchor.png' | relative_url }}" alt="Morie Anchor icon">
        </div>
        <h3>Morie Anchor</h3>
        <p>
          Advanced anchor engineering for offshore anchor points, covering pile and plate types.
          Supports extreme and cyclic capacity assessment, load transfer, installation checks,
          soil-dependent and seismic design workflows.
        </p>
      </div>

      <div class="capability-card">
        <div class="capability-card__icon">
          <img src="{{ '/img/morie_icon_atlas.png' | relative_url }}" alt="Morie Atlas icon">
        </div>
        <h3>Morie Atlas</h3>
        <p>
          A spatial and automated intelligence platform for mapping offshore floating anchor designs across
          lease areas, integrating bathymetry, soil data and system response into decision-ready site views.
          Enables sharp and quick comparison for feasibility and cost studies.
        </p>
      </div>

      <div class="capability-card">
        <div class="capability-card__icon">
          <img src="{{ '/img/morie_icon_GAN.png' | relative_url }}" alt="Morie SchemaGAN icon">
        </div>
        <h3>Morie SchemaGAN</h3>
        <p>
          A synthetic subsurface generation framework enabling data-driven reconstruction of offshore ground
          models based on Generative Adversarial Networks. Supports soil characterization, uncertainty
          exploration and improves early-stage engineering studies.
        </p>
      </div>

    </div>
  </div>
</section>

<!-- ── PORTFOLIO ──────────────────────────────────────────────────────── -->
<section class="portfolio-page" id="portfolio" aria-label="Engineering portfolio">
  <div class="container portfolio-container">

    <div class="portfolio-page__intro">
      <p class="home-storyband__eyebrow">Portfolio</p>
      <h2 class="plat-section__title">Celtic Sea floating wind — end-to-end workflow</h2>

      <p class="portfolio-page__lead">
        A system-level engineering portfolio for floating offshore wind, integrating site intelligence, layout optimization,
        soil reconstruction, mooring physics, anchor design and cable performance into a unified workflow.
      </p>

      <p class="portfolio-page__lead">
        The framework builds on and extends research foundations established in floating offshore wind studies at the
        National Renewable Energy Laboratory (NREL), translating them into a practical, engineering-driven workflow
        for real-world applications. Each study case represents a connected layer in the design chain, demonstrating
        how data, physics and scalable computation combine to drive robust, cost-efficient offshore wind solutions.
      </p>

      <p class="portfolio-page__workflow">
        <strong>Site Intelligence ↔ Layout Optimization ↔ Soil Reconstruction ↔ Mooring Physics ↔ Anchor Design ↔ Cable Performance</strong>
      </p>
    </div>

    <div class="row">
      {% assign desired_order = 'morie_site|morie_layout|morie_soil|morie_mooring|morie_anchor|morie_cable' | split: '|' %}

      {% for target_slug in desired_order %}
        {% for post in site.posts %}
          {% if post.slug == target_slug %}
            {% include post-card.html %}
          {% endif %}
        {% endfor %}
      {% endfor %}
    </div>

  </div>
</section>

<!-- ── CTA ───────────────────────────────────────────────────────────── -->
<section class="plat-access" aria-label="Contact call to action">
  <div class="plat-container">
    <div class="plat-access__header">
      <p class="home-storyband__eyebrow">Work with us</p>
      <h2 class="plat-section__title plat-section__title--light">Ready to work together?</h2>
      <p class="plat-access__lead">
        Whether you need targeted engineering studies, system-level support or longer-term technical integration,
        we are here to help. Get in touch to discuss your project.
      </p>
      <a href="{{ '/contact/' | relative_url }}" class="hero-button hero-button--secondary">Contact us</a>
    </div>
  </div>
</section>
