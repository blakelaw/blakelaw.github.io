---
layout: archive
title: "Gallery"
permalink: /gallery/
author_profile: true
---

{% include base_path %}

Welcome to my gallery of data visualizations. Click to view in full size.

<div class="gallery" style="display: grid; grid-template-columns: repeat(auto-fill, minmax(250px, 1fr)); gap: 15px;">
  {% for file in site.static_files %}
    {% if file.path contains 'images/Charts' %}
      <div class="gallery-item" style="position: relative; overflow: hidden;">
        <a href="{{ file.path | prepend: site.baseurl }}" data-toggle="lightbox" data-gallery="gallery" data-type="image">
          <img src="{{ file.path | prepend: site.baseurl }}" alt="Chart" class="img-responsive" style="transition: transform .2s; width: 100%; height: auto;">
        </a>
      </div>
    {% endif %}
  {% endfor %}
</div>

<script>
document.addEventListener('DOMContentLoaded', (event) => {
  document.querySelectorAll('.gallery-item').forEach((item) => {
    item.addEventListener('mouseenter', (e) => {
      e.currentTarget.querySelector('img').style.transform = 'scale(1.1)';
    });
    item.addEventListener('mouseleave', (e) => {
      e.currentTarget.querySelector('img').style.transform = 'scale(1)';
    });
  });
});
</script>
