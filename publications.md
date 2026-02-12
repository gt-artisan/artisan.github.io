---
title: "Publications — ARTISAN"
---

# Publications

{% comment %}
Reads _data/publications.yml (top-level array recommended).
Fields supported: title, authors (list or string), venue, year, doi, url, pdf, arxiv
This template is Liquid-safe (every block is properly closed).
{% endcomment %}

{% assign pubs = site.data.publications | default: empty %}

{% if pubs and pubs.size > 0 %}

  {%- comment -%} Sort newest year first and build a unique list of years {%- endcomment -%}
  {% assign pubs_sorted = pubs | sort: "year" | reverse %}
  {% assign years = pubs_sorted | map: "year" | uniq %}

  {% for y in years %}
  ## {{ y }}

  <div class="grid">
    {% for p in pubs_sorted %}
      {% if p.year == y %}
      <article class="card">
        <h3 class="text-navy" style="margin-bottom:.25rem;">{{ p.title }}</h3>

        {%- comment -%} Authors line (works if authors is a list OR string) {%- endcomment -%}
        {% if p.authors %}
          {% if p.authors.first %}
            <p style="margin:.25rem 0;"><em>{{ p.authors | join: ", " }}</em></p>
          {% else %}
            <p style="margin:.25rem 0;"><em>{{ p.authors }}</em></p>
          {% endif %}
        {% endif %}

        {%- comment -%} Venue + year (redundant but fine inside the card) {%- endcomment -%}
        <p style="margin:.25rem 0;">
          {% if p.venue %}<span>{{ p.venue }}</span>{% endif %}
          {% if p.venue and p.year %} · {% endif %}
          {% if p.year %}<span>{{ p.year }}</span>{% endif %}
        </p>

        {%- comment -%} Links row (show only those that exist) {%- endcomment -%}
        {% assign has_prev = false %}
        <p style="margin:.25rem 0;">
          {% if p.doi %}
            {{ "https://doi.org/" | append: p.doi }}DOI</a>
            {% assign has_prev = true %}
          {% endif %}

          {% if p.arxiv %}
            {% if has_prev %} · {% endif %}
            {{ p.arxiv }}arXiv</a>
            {% assign has_prev = true %}
          {% endif %}

          {% if p.url %}
            {% if has_prev %} · {% endif %}
            {{ p.url }}Link</a>
            {% assign has_prev = true %}
          {% endif %}

          {% if p.pdf %}
            {% if has_prev %} · {% endif %}
            {{ p.pdf }}PDF</a>
          {% endif %}
        </p>
      </article>
      {% endif %}
    {% endfor %}
  </div>

  {% endfor %}

{% else %}
  <p>No publications found. Ensure <code>_data/publications.yml</code> exists and contains an array of entries.</p>
{% endif %}