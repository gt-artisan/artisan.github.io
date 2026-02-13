---
title: "Publications — ARTISAN"
---

# Publications

<label for="yearFilter" class="text-navy" style="font-weight:600;">Filter by year:</label>
<select id="yearFilter" onchange="filterYear()">
  <option value="all">All years</option>
  {% for y in years %}
    <option value="{{ y }}">{{ y }}</option>
  {% endfor %}
</select>

<script>
function filterYear() {
  const sel = document.getElementById('yearFilter').value;
  document.querySelectorAll('.pub-year').forEach((h2) => {
    const sectionGrid = h2.nextElementSibling;
    const show = (sel === 'all' || h2.textContent.trim() === sel);
    h2.style.display = show ? 'block' : 'none';
    if (sectionGrid) sectionGrid.style.display = show ? 'grid' : 'none';
  });
}
</script>

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

<script type="application/ld+json">
{
  "@context":"https://schema.org",
  "@type":"ItemList",
  "itemListElement": [
    {% for p in pubs_sorted %}
    {
      "@type":"ScholarlyArticle",
      "name": {{ p.title | jsonify }},
      {% if p.authors %}
      "author": [{% if p.authors.first %}{% for a in p.authors %}{"@type":"Person","name":{{ a | jsonify }}}{% unless forloop.last %},{% endunless %}{% endfor %}{% else %}{"@type":"Person","name":{{ p.authors | jsonify }}}{% endif %}],
      {% endif %}
      {% if p.venue %}"isPartOf":{"@type":"Periodical","name":{{ p.venue | jsonify }}},{% endif %}
      {% if p.year %}"datePublished":"{{ p.year }}",{% endif %}
      {% if p.doi %}"identifier":"https://doi.org/{{ p.doi }}",{% endif %}
      {% if p.url %}"url": {{ p.url | jsonify }},{% endif %}
      {% if p.pdf %}"encoding":{"@type":"MediaObject","contentUrl": {{ p.pdf | jsonify }} }{% endif %}
    }{% unless forloop.last %},{% endunless %}
    {% endfor %}
  ]
}
</script>