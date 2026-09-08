---
layout: page
title: Software
permalink: /software/
toggle: on
rank: 3
---

{% assign software_categories = site.data.softwares %}
{% assign total_tools = 0 %}
{% for category in software_categories %}
  {% assign total_tools = total_tools | plus: category.tools.size %}
{% endfor %}

<section class="software-page" id="software">
  <div class="software-hero">
    <p class="eyebrow">MDOP-Labs toolkit</p>
    <h1>Software</h1>
    <p>
      Software is organized into three working tracks aligned with the laboratory's projects,
      theses, publications, and congress presentations: reproducible development, cancer omics,
      and protein-structure modeling for molecular dynamics and oncology progression.
    </p>
    <p class="software-source">
      Includes curated starting points such as MitoMatch, Tabula Sapiens 2.0, TISCH2,
      OMIM, AlphaMissense, and complementary tools for building reproducible workflows.
    </p>
  </div>

  <div class="software-controls" aria-label="Software filters">
    <div class="control-block">
      <h2>Area</h2>
      <div class="software-tabs" role="tablist" aria-label="Software area tabs">
        {% for category in software_categories %}
          <button class="software-tab{% if forloop.first %} active{% endif %}" type="button" role="tab" aria-selected="{% if forloop.first %}true{% else %}false{% endif %}" data-category="{{ category.category }}">
            {{ category.label }} <span>{{ category.tools.size }}</span>
          </button>
        {% endfor %}
      </div>
    </div>

    <div class="control-block software-summary-block">
      <h2>Summary</h2>
      <p>
        Showing <strong>{{ total_tools }}</strong> tools across <strong>{{ software_categories.size }}</strong> tracks.
        Each card includes a purpose, a first action, tags, and a direct source link.
      </p>
    </div>
  </div>

  <p class="software-filter-status" aria-live="polite">
    Showing {{ software_categories.first.tools.size }} tools · Area: {{ software_categories.first.label }}.
  </p>

  <section class="software-panels">
    {% for category in software_categories %}
      <article class="software-panel{% if forloop.first %} active{% endif %}" data-category-panel="{{ category.category }}" data-category-label="{{ category.label }}" data-tool-count="{{ category.tools.size }}">
        <div class="software-panel-heading">
          <div>
            <p class="eyebrow">Track {{ forloop.index }}</p>
            <h2>{{ category.label }}</h2>
            <p class="software-tagline">{{ category.tagline }}</p>
          </div>
        </div>

        <p class="software-focus">{{ category.focus }}</p>

        <div class="software-tool-grid">
          {% for tool in category.tools %}
            <article class="software-tool-card">
              <div class="software-tool-topline">
                <span class="software-category software-category-{{ category.category }}">{{ category.label }}</span>
                <a class="software-tool-link" href="{{ tool.url }}" target="_blank" rel="noopener noreferrer" aria-label="Open {{ tool.name }}">Open ↗</a>
              </div>

              <h3><a href="{{ tool.url }}" target="_blank" rel="noopener noreferrer">{{ tool.name }}</a></h3>
              <p class="software-purpose">{{ tool.purpose }}</p>

              <dl class="software-details">
                <div>
                  <dt>Start with</dt>
                  <dd>{{ tool.start }}</dd>
                </div>
                {% if tool.tags %}
                  <div>
                    <dt>Tags</dt>
                    <dd>
                      <span class="software-tags">
                        {% for tag in tool.tags %}
                          <span>{{ tag }}</span>
                        {% endfor %}
                      </span>
                    </dd>
                  </div>
                {% endif %}
              </dl>
            </article>
          {% endfor %}
        </div>
      </article>
    {% endfor %}
  </section>

  <section class="software-roadmap">
    <h2>How to begin</h2>
    <div class="software-roadmap-grid">
      <article>
        <strong>1. Convert ideas into reproducible projects.</strong>
        <p>Start with Git/GitHub, Conda or Docker, and a small notebook or command-line workflow before scaling to Snakemake, Nextflow, or a Streamlit app.</p>
      </article>
      <article>
        <strong>2. Anchor omics hypotheses in public evidence.</strong>
        <p>Use TISCH2, Tabula Sapiens 2.0, GDC, GEO, cBioPortal, OMIM, Open Targets, MitoMatch, and AlphaMissense to define genes, cohorts, cell states, and variants before local analysis.</p>
      </article>
      <article>
        <strong>3. Connect variants and pathways to structure.</strong>
        <p>Move from RCSB or AlphaFold models to Boltz-2, docking, membrane-system setup, molecular dynamics, and interaction profiling when a mechanistic structural question is justified.</p>
      </article>
    </div>
  </section>
</section>

<style>
  .software-page {
    --project-blue: #003c71;
    --project-orange: #e69635;
    --project-ink: #243447;
    --project-muted: #687386;
    --project-border: #dfe7f0;
    --project-bg: #f7fafc;
    --project-green: #357a38;
    --project-purple: #6b4bb8;
    --project-black: #24292f;
  }

  .software-hero {
    padding: 1.5rem;
    margin-bottom: 1.5rem;
    border: 1px solid var(--project-border);
    border-left: 6px solid var(--project-orange);
    border-radius: 16px;
    background: linear-gradient(135deg, #ffffff 0%, var(--project-bg) 100%);
  }

  .software-hero .eyebrow,
  .software-panel .eyebrow {
    margin: 0 0 0.35rem;
    color: var(--project-orange);
    font-size: 0.78rem;
    font-weight: 800;
    letter-spacing: 0.08em;
    text-transform: uppercase;
  }

  .software-hero h1 {
    margin: 0 0 0.6rem;
    color: var(--project-blue);
  }

  .software-hero p {
    max-width: 820px;
    margin-bottom: 0.55rem;
    color: var(--project-ink);
  }

  .software-source {
    font-size: 0.92rem;
    color: var(--project-muted) !important;
  }

  .software-controls {
    display: grid;
    grid-template-columns: 1fr;
    gap: 1rem;
    margin-bottom: 0.85rem;
  }

  .control-block {
    padding: 1rem;
    border: 1px solid var(--project-border);
    border-radius: 14px;
    background: #fff;
  }

  .control-block h2 {
    margin: 0 0 0.75rem;
    color: var(--project-blue);
    font-size: 1rem;
  }

  .software-summary-block p {
    margin: 0;
    color: var(--project-ink);
  }

  .software-tabs {
    display: flex;
    flex-wrap: wrap;
    gap: 0.55rem;
  }

  .software-tab {
    cursor: pointer;
    border: 1px solid var(--project-border);
    border-radius: 999px;
    padding: 0.55rem 0.9rem;
    background: #fff;
    color: var(--project-blue);
    font-weight: 800;
    line-height: 1;
    transition: background 0.18s ease, border-color 0.18s ease, color 0.18s ease, transform 0.18s ease;
  }

  .software-tab span {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    min-width: 1.35rem;
    margin-left: 0.35rem;
    padding: 0.18rem 0.35rem;
    border-radius: 999px;
    background: var(--project-bg);
    color: var(--project-muted);
    font-size: 0.78rem;
  }

  .software-tab:hover,
  .software-tab:focus {
    border-color: var(--project-orange);
    transform: translateY(-1px);
  }

  .software-tab.active {
    border-color: var(--project-blue);
    background: var(--project-blue);
    color: #fff;
  }

  .software-tab.active span {
    background: rgba(255, 255, 255, 0.18);
    color: #fff;
  }

  .software-filter-status {
    color: var(--project-muted);
    font-size: 0.92rem;
  }

  .software-panel {
    display: none;
  }

  .software-panel.active {
    display: block;
  }

  .software-panel-heading {
    margin-bottom: 0.75rem;
  }

  .software-panel h2,
  .software-roadmap h2 {
    margin: 0 0 0.6rem;
    color: var(--project-blue);
  }

  .software-tagline,
  .software-focus {
    color: var(--project-ink);
  }

  .software-focus {
    max-width: 920px;
    margin: 0 0 1rem;
  }

  .software-tool-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1rem;
  }

  .software-tool-card {
    display: flex;
    flex-direction: column;
    gap: 0.8rem;
    min-height: 100%;
    padding: 1rem;
    border: 1px solid var(--project-border);
    border-top: 4px solid var(--project-orange);
    border-radius: 14px;
    background: #fff;
    box-shadow: 0 8px 22px rgba(0, 60, 113, 0.07);
  }

  .software-tool-topline {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: space-between;
    gap: 0.45rem;
  }

  .software-category,
  .software-tool-link {
    border-radius: 999px;
    padding: 0.25rem 0.58rem;
    font-size: 0.72rem;
    font-weight: 800;
    letter-spacing: 0.01em;
  }

  .software-category {
    background: rgba(0, 60, 113, 0.1);
    color: var(--project-blue);
  }

  .software-category-omics {
    background: rgba(53, 122, 56, 0.13);
    color: var(--project-green);
  }

  .software-category-protein-structure {
    background: rgba(107, 75, 184, 0.13);
    color: var(--project-purple);
  }

  .software-tool-link {
    background: var(--project-bg);
    color: var(--project-muted);
    text-decoration: none;
  }

  .software-tool-card h3 {
    margin: 0;
    color: var(--project-blue);
    font-size: 1.05rem;
    line-height: 1.35;
  }

  .software-tool-card h3 a {
    color: inherit;
    text-decoration: none;
  }

  .software-tool-card h3 a:hover,
  .software-tool-link:hover {
    color: var(--project-orange);
    text-decoration: underline;
  }

  .software-purpose {
    margin: 0;
    color: var(--project-ink);
  }

  .software-details {
    display: grid;
    gap: 0.55rem;
    margin: auto 0 0;
  }

  .software-details div {
    padding-top: 0.55rem;
    border-top: 1px solid var(--project-border);
  }

  .software-details dt {
    color: var(--project-muted);
    font-size: 0.72rem;
    font-weight: 800;
    letter-spacing: 0.06em;
    text-transform: uppercase;
  }

  .software-details dd {
    margin: 0.15rem 0 0;
    color: var(--project-ink);
  }

  .software-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 0.35rem;
  }

  .software-tags span {
    display: inline-flex;
    border-radius: 999px;
    padding: 0.2rem 0.48rem;
    background: var(--project-bg);
    color: var(--project-muted);
    font-size: 0.72rem;
    font-weight: 800;
  }

  .software-roadmap {
    margin-top: 1.5rem;
    padding: 1rem;
    border: 1px solid var(--project-border);
    border-radius: 14px;
    background: #fff;
  }

  .software-roadmap-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1rem;
  }

  .software-roadmap article {
    padding: 1rem;
    border: 1px solid var(--project-border);
    border-top: 4px solid var(--project-orange);
    border-radius: 14px;
    background: #fff;
    box-shadow: 0 8px 22px rgba(0, 60, 113, 0.07);
  }

  .software-roadmap strong {
    color: var(--project-blue);
  }

  .software-roadmap p {
    margin: 0.55rem 0 0;
    color: var(--project-ink);
  }

  @media (min-width: 780px) {
    .software-controls {
      grid-template-columns: 1.05fr 0.95fr;
    }
  }

  @media (max-width: 640px) {
    .software-hero,
    .control-block,
    .software-roadmap {
      padding: 1rem;
    }

    .software-tool-grid,
    .software-roadmap-grid {
      grid-template-columns: 1fr;
    }
  }
</style>

<script>
  (function () {
    var tabs = Array.prototype.slice.call(document.querySelectorAll('.software-tab'));
    var panels = Array.prototype.slice.call(document.querySelectorAll('[data-category-panel]'));
    var status = document.querySelector('.software-filter-status');
    var activeCategory = tabs.length ? tabs[0].getAttribute('data-category') : '';

    function applyCategory(category) {
      activeCategory = category;
      var activePanel = null;

      tabs.forEach(function (button) {
        var isActive = button.getAttribute('data-category') === activeCategory;
        button.classList.toggle('active', isActive);
        button.setAttribute('aria-selected', isActive ? 'true' : 'false');
      });

      panels.forEach(function (panel) {
        var isActive = panel.getAttribute('data-category-panel') === activeCategory;
        panel.classList.toggle('active', isActive);
        if (isActive) {
          activePanel = panel;
        }
      });

      if (status && activePanel) {
        status.textContent = 'Showing ' + activePanel.getAttribute('data-tool-count') + ' tools · Area: ' + activePanel.getAttribute('data-category-label') + '.';
      }
    }

    tabs.forEach(function (button) {
      button.addEventListener('click', function () {
        applyCategory(button.getAttribute('data-category'));
      });
    });
  })();
</script>
