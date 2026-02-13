---
title: "Publications — ARTISAN"
---

# Publications

{% assign pubs = site.data.publications | default: empty %}

{% if pubs and pubs.size > 0 %}
  {% assign pubs_sorted = pubs | sort: "year" | reverse %}
  {% assign years = pubs_sorted | map: "year" | uniq %}

  {% for y in years %}
  <h2 class="pub-year">{{ y }}</h2>

  <div class="grid">
    {% for p in pubs_sorted %}
      {% if p.year == y %}
      <article class="pub-card card">

        <div class="pub-title">{{ p.title }}</div>

        {% if p.authors %}
          {% if p.authors.first %}
            <div class="pub-authors"><em>{{ p.authors | join: ", " }}</em></div>
          {% else %}
            <div class="pub-authors"><em>{{ p.authors }}</em></div>
          {% endif %}
        {% endif %}

        <div class="pub-meta">
          {% if p.venue %}{{ p.venue }}{% endif %}
          {% if p.year %} · {{ p.year }}{% endif %}
        </div>

        <div class="pub-links">
          {% if p.doi %}
            <a class="pub-link" href="https://doi.org/{{ p.doi }}" target="_blank">DOI</a>
          {% endif %}
          {% if p.arxiv %}
            <a class="pub-link" href="https://arxiv.org/abs/{{ p.arxiv }}" target="_blank">arXiv</a>
          {% endif %}
          {% if p.url %}
            <a class="pub-link" href="{{ p.url }}" target="_blank">Link</a>
          {% endif %}
          {% if p.pdf %}
            <a class="pub-link" href="{{ p.pdf }}" target="_blank">PDF</a>
          {% endif %}
        </div>

      </article>
      {% endif %}
    {% endfor %}
  </div>

  {% endfor %}
{% else %}
  <p>No publications found.</p>
{% endif %}