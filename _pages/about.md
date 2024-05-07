---
layout: about
permalink: /about/
title: about
subtitle: The DanceCam initiative aims at improving astronomical wide-field imaging from the ground, using a combination of machine learning and high resolution video streams of the deep sky.
nav: true
nav_order: 1
profile:
   align: left
   image: dancecam_logo.png
   more_info: 

social: true # includes social icons at the bottom of the page
horizontal: true
---

### Video imaging offers many advantages over conventional long exposures:

<!-- pages/about2.md -->
<div class="projects" style="margin-top: 2rem;">
<!-- Display projects without categories -->
{% assign sorted_projects = site.benefits | sort: "importance" %}

  <!-- Generate cards for each project -->

{% if page.horizontal %}

  <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
    {% for project in sorted_projects %}
      {% include benefits.liquid %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for project in sorted_projects %}
      {% include benefits.liquid %}
    {% endfor %}
  </div>
  {% endif %}
</div>

