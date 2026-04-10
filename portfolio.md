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
		A system-level engineering portfolio for floating offshore wind, integrating site intelligence, layout optimization, 
		soil reconstruction, mooring physics, anchor design and cable performance into a unified workflow.	
      </p>

      <p class="portfolio-page__lead">
		The framework builds on and extends research foundations established in floating offshore wind studies at NREL, 
		translating them into a practical, engineering-driven workflow for real-world applications. Each study case represents 
		a connected layer in the design chain, demonstrating how data, physics, and scalable computation combine to drive robust, cost-efficient offshore wind solutions.
      </p>

      <p class="portfolio-page__workflow">
        <strong>Site Intelligence → Layout Optimization → Soil Reconstruction → Mooring Physics → Anchor Design → Cable Performance</strong>
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