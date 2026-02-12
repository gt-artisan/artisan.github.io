---
title: "ARTISAN — Georgia Tech"
---

<section class="bg-navy section">
  <div class="container">
    <h1 class="gt-gold" style="margin-bottom:.25rem;">Center for Artificial Intelligence in Science & Engineering</h1>
    <p style="max-width:65ch;color:#E6EDF5;">
      A joint Center between the College of Computing and the Institute for Data Engineering and Science dedicated to accelerating science & engineering with AI, cyberinfrastructure, and open platforms.
    </p>
    /research" class="btn btn--gold">Explore Research</a>
    /projects" class="btn" style="margin-left:.5rem;">View Projects</a>
  </div>
</section>

<section class="section">
  <div class="container">
    <h2 class="text-navy">Latest News & Events</h2>
    <div class="grid">
      {% assign latest_news = site.news | sort: "date" | reverse | slice: 0,3 %}
      {% for post in latest_news %}
      <article class="card">
        {{ post.title }}</a>
        <p style="margin:.25rem 0 .5rem 0; color:#666;">{{ post.date | date: "%b %d, %Y" }}</p>
        <p>{{ post.excerpt }}</p>
      </article>
      {% endfor %}
    </div>
  </div>
</section>

<section class="section section--alt">
  <div class="container">
    <h2 class="text-navy">Research Areas</h2>
    <div class="grid">
      <div class="card">
        /research#ci" class="text-navy"><strong>Cyberinfrastructure & Distributed Systems</strong></a>
        <p>Scalable, high-performance systems powering AI and scientific research.</p>
      </div>
      <div class="card">
        /research#ai-se" class="text-navy"><strong>AI-Driven Solutions for S&E</strong></a>
        <p>Domain-tailored AI/ML for protein modeling, quantum chemistry, climate, neuroscience.</p>
      </div>
      <div class="card">
        /research#interpretable" class="text-navy"><strong>Interpretable AI for Discovery</strong></a>
        <p>Accurate predictions with insight to advance scientific theories and knowledge.</p>
      </div>
    </div>
  </div>
</section>