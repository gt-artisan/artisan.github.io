---
title: "ARTISAN Team — Georgia Tech"
---

# ARTISAN Team

<div class="grid">
{% for person in site.data.team %}
  <div class="card">
    <h3 class="text-navy" style="margin-bottom:.25rem;">{{ person.name }}</h3>
    <p style="margin-top:0;">{{ person.title }}</p>
    <p>
    {% if person.scholar %} {{ person.scholar }}</a>{% endif %}
    {% if person.linkedin %} · {{ person.linkedin }}</a>{% endif %}
    </p>
  </div>
{% endfor %}
</div>