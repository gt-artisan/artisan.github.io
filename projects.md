---
title: "Projects — ARTISAN"
---

# Projects

<div class="grid">
{% for item in site.data.projects %}
  <article class="card">
    <h3 class="text-navy">{{ item.name }}</h3>
    <p>{{ item.blurb }}</p>
    {{ item.url }}</a>
  </article>
{% endfor %}
</div>