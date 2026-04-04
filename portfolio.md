---
layout: default
title: Portfolio
permalink: /portfolio/
---

<section class="portfolio-page">
  <div class="container portfolio-container">

    <div class="portfolio-page__intro">
      <h1>Offshore Wind Engineering Portfolio</h1>

      <p class="portfolio-page__lead">
        A collection of interconnected study cases covering the full engineering workflow
        for floating offshore wind systems.
      </p>

      <p>
        Each case represents a key layer in the design chain, from site characterization
        to subsystem optimization.
      </p>

      <p class="portfolio-page__workflow">
        <strong>Site → Layout → Soil → Mooring → Anchor → Cable</strong>
      </p>
    </div>

    <div class="row">
      {% assign desired_order = 'Lease Area Site Characterization – Celtic Sea|Layout Generation & Topology Optimization – Celtic Sea|Local Soil Reconstruction & Subsurface Intelligence – Celtic Sea|Mooring System Generation & Load Analysis – Celtic Sea|Shared Anchor Load Resolution & Capacity Verification – Celtic Sea|Dynamic Cable Design & Optimization – Celtic Sea' | split: '|' %}

      {% for target_title in desired_order %}
        {% for post in site.posts %}
          {% if post.title == target_title %}
            {% include post-card.html %}
          {% endif %}
        {% endfor %}
      {% endfor %}
    </div>

  </div>
</section>