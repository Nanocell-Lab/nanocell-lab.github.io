---
layout: page
title: Publications
permalink: /publications/
toggle: on
rank: 4
---

{% assign publications_by_year = site.data.publications | group_by: "year" | sort: "name" | reverse %}
{% assign total_publications = site.data.publications | size %}

<section class="publications-page" id="publications">
  <div class="publications-hero">
    <p class="eyebrow">Producción científica desde 2020</p>
    <h1>Publicaciones</h1>
    <p>
      Selección actualizada desde la ficha académica de Postgrado UdeC de Alexis Marcelo Salas Burgos.
      Usa el filtro para desplegar publicaciones por año.
    </p>
    <p class="publication-source">
      Fuente:
      <a href="https://postgrado.udec.cl/catalogo/academico/alexis-marcelo-salas-burgos" target="_blank" rel="noopener noreferrer">
        Catálogo Académico Postgrado UdeC
      </a>
    </p>
  </div>

  <div class="publication-toolbar" aria-label="Filtro de publicaciones por año">
    <button class="year-filter active" type="button" data-year="all" aria-pressed="true">
      Todas <span>{{ total_publications }}</span>
    </button>
    {% for year_group in publications_by_year %}
      <button class="year-filter" type="button" data-year="{{ year_group.name }}" aria-pressed="false">
        {{ year_group.name }} <span>{{ year_group.items | size }}</span>
      </button>
    {% endfor %}
  </div>

  <p class="publication-filter-status" aria-live="polite">
    Mostrando {{ total_publications }} publicaciones desde 2020.
  </p>

  <div class="publication-year-groups">
    {% for year_group in publications_by_year %}
      <section class="publication-year-group" data-year-group="{{ year_group.name }}">
        <div class="year-heading">
          <h2>{{ year_group.name }}</h2>
          <span>{{ year_group.items | size }} publicaciones</span>
        </div>

        <div class="publication-grid">
          {% for publication in year_group.items %}
            <article class="publication-card" data-year="{{ publication.year }}">
              <div class="publication-card-header">
                <span class="publication-year">{{ publication.year }}</span>
                <span class="publication-type">{{ publication.type }}</span>
              </div>

              <h3>
                {% if publication.url %}
                  <a href="{{ publication.url }}" target="_blank" rel="noopener noreferrer">{{ publication.title }}</a>
                {% else %}
                  {{ publication.title }}
                {% endif %}
              </h3>

              <div class="publication-meta">
                <span>{{ publication.journal }}</span>
                {% if publication.indexing %}
                  <span>{{ publication.indexing }}</span>
                {% endif %}
                {% if publication.role %}
                  <span>{{ publication.role }}</span>
                {% endif %}
              </div>
            </article>
          {% endfor %}
        </div>
      </section>
    {% endfor %}
  </div>
</section>

<style>
  .publications-page {
    --pub-blue: #003c71;
    --pub-orange: #e69635;
    --pub-ink: #243447;
    --pub-muted: #687386;
    --pub-border: #dfe7f0;
    --pub-bg: #f7fafc;
  }

  .publications-hero {
    padding: 1.5rem;
    margin-bottom: 1.5rem;
    border: 1px solid var(--pub-border);
    border-left: 6px solid var(--pub-orange);
    border-radius: 16px;
    background: linear-gradient(135deg, #ffffff 0%, var(--pub-bg) 100%);
  }

  .publications-hero .eyebrow {
    margin: 0 0 0.35rem;
    color: var(--pub-orange);
    font-size: 0.78rem;
    font-weight: 700;
    letter-spacing: 0.08em;
    text-transform: uppercase;
  }

  .publications-hero h1 {
    margin: 0 0 0.6rem;
    color: var(--pub-blue);
  }

  .publications-hero p {
    max-width: 760px;
    margin-bottom: 0.55rem;
    color: var(--pub-ink);
  }

  .publication-source {
    font-size: 0.92rem;
  }

  .publication-toolbar {
    display: flex;
    flex-wrap: wrap;
    gap: 0.55rem;
    margin: 0 0 0.75rem;
  }

  .year-filter {
    cursor: pointer;
    border: 1px solid var(--pub-border);
    border-radius: 999px;
    padding: 0.55rem 0.9rem;
    background: #fff;
    color: var(--pub-blue);
    font-weight: 700;
    line-height: 1;
    transition: background 0.18s ease, border-color 0.18s ease, color 0.18s ease, transform 0.18s ease;
  }

  .year-filter span {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    min-width: 1.35rem;
    margin-left: 0.35rem;
    padding: 0.18rem 0.35rem;
    border-radius: 999px;
    background: var(--pub-bg);
    color: var(--pub-muted);
    font-size: 0.78rem;
  }

  .year-filter:hover,
  .year-filter:focus {
    border-color: var(--pub-orange);
    transform: translateY(-1px);
  }

  .year-filter.active {
    border-color: var(--pub-blue);
    background: var(--pub-blue);
    color: #fff;
  }

  .year-filter.active span {
    background: rgba(255, 255, 255, 0.18);
    color: #fff;
  }

  .publication-filter-status {
    color: var(--pub-muted);
    font-size: 0.92rem;
  }

  .publication-year-group {
    margin-top: 2rem;
  }

  .year-heading {
    display: flex;
    align-items: baseline;
    justify-content: space-between;
    gap: 1rem;
    margin-bottom: 0.85rem;
    border-bottom: 2px solid var(--pub-border);
  }

  .year-heading h2 {
    margin-bottom: 0.35rem;
    color: var(--pub-blue);
  }

  .year-heading span {
    color: var(--pub-muted);
    font-size: 0.9rem;
    white-space: nowrap;
  }

  .publication-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
    gap: 1rem;
  }

  .publication-card {
    display: flex;
    flex-direction: column;
    gap: 0.75rem;
    min-height: 100%;
    padding: 1rem;
    border: 1px solid var(--pub-border);
    border-top: 4px solid var(--pub-orange);
    border-radius: 14px;
    background: #fff;
    box-shadow: 0 8px 22px rgba(0, 60, 113, 0.07);
  }

  .publication-card-header,
  .publication-meta {
    display: flex;
    flex-wrap: wrap;
    gap: 0.4rem;
  }

  .publication-year,
  .publication-type,
  .publication-meta span {
    border-radius: 999px;
    padding: 0.25rem 0.55rem;
    font-size: 0.72rem;
    font-weight: 700;
    letter-spacing: 0.01em;
  }

  .publication-year {
    background: rgba(0, 60, 113, 0.1);
    color: var(--pub-blue);
  }

  .publication-type {
    background: rgba(230, 150, 53, 0.14);
    color: #8a4c0c;
  }

  .publication-card h3 {
    margin: 0;
    color: var(--pub-ink);
    font-size: 1.02rem;
    line-height: 1.35;
  }

  .publication-card h3 a {
    color: var(--pub-blue);
  }

  .publication-meta {
    margin-top: auto;
  }

  .publication-meta span {
    background: var(--pub-bg);
    color: var(--pub-muted);
  }

  .publication-year-group.is-hidden {
    display: none;
  }

  @media (max-width: 640px) {
    .publications-hero {
      padding: 1rem;
    }

    .year-heading {
      display: block;
    }

    .publication-grid {
      grid-template-columns: 1fr;
    }
  }
</style>

<script>
  (function () {
    var buttons = Array.prototype.slice.call(document.querySelectorAll('.year-filter'));
    var groups = Array.prototype.slice.call(document.querySelectorAll('.publication-year-group'));
    var status = document.querySelector('.publication-filter-status');
    var total = {{ total_publications }};

    function setYear(year) {
      var shown = 0;

      buttons.forEach(function (button) {
        var isActive = button.getAttribute('data-year') === year;
        button.classList.toggle('active', isActive);
        button.setAttribute('aria-pressed', isActive ? 'true' : 'false');
      });

      groups.forEach(function (group) {
        var matches = year === 'all' || group.getAttribute('data-year-group') === year;
        group.classList.toggle('is-hidden', !matches);
        if (matches) {
          shown += group.querySelectorAll('.publication-card').length;
        }
      });

      if (status) {
        status.textContent = year === 'all'
          ? 'Mostrando ' + total + ' publicaciones desde 2020.'
          : 'Mostrando ' + shown + ' publicaciones de ' + year + '.';
      }
    }

    buttons.forEach(function (button) {
      button.addEventListener('click', function () {
        setYear(button.getAttribute('data-year'));
      });
    });
  })();
</script>
