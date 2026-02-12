---
title: "Scientific Software — ARTISAN"
---

# Scientific Software

<div class="grid">
{% for s in site.data.software %}
  <article class="card">
    <h3 class="text-navy">{{ s.name }}</h3>
    <p>{{ s.desc }}</p>
    {{ s.url }}</a>
  </article>
{% endfor %}
</div>