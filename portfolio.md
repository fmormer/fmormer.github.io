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