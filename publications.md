---
title: "Publications — ARTISAN"
---

# Publications

{% comment %}
We group by year (desc), then print items newest-first within each year.
The YAML (generated from BibTeX) lives in site.data.publications.
{% endcomment %}

{% assign pubs = site.data.publications | default: empty %}
{% if pubs and pubs.size > 0 %}
  {% assign pubs_sorted = pubs | sort: "year" | reverse %}
  {% assign years = pubs_sorted | map: "year" | uniq %}

  {% for y in years %}
  ## {{ y }}
  <ul>
    {% for p in pubs_sorted %}
      {% if p.year == y %}
        <li style="margin-bottom:.5rem;">
          <strong>{{ p.title }}</strong>
          {% if p.authors and p.authors.size > 0 %}
            <br/><em>{{ p.authors | join: ", " }}</em>
          {% endif %}
          {% if p.venue %} — {{ p.venue }}{% endif %}
          {% if p.doi %} · DOI: {{ p.doi }}{% endif %}
          {% if p.arxiv %} · arXiv: {{ p.arxiv }}{% endif %}
          {% if p.url %} · {{ p.url }}</a>{% endif %}
          {% if p.pdf %} · {{ p.pdf }}</a>{% endif %}
        </li>
      {% endif %}
    {% endfor %}
  </ul>
  {% endfor %}
{% else %}
  <p>No publications listed yet. Add items to <code>_data/publications.bib</code>.</p>
{% endif %}