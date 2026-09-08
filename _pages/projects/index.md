---
layout: page
title: Projects
permalink: /projects/
toggle: on
rank: 1
---

{% assign projects_by_year = site.data.projects | group_by: "start_year" | sort: "name" | reverse %}
{% assign total_projects = site.data.projects | size %}
{% assign fondecyt_projects = site.data.projects | where: "category", "fondecyt" %}
{% assign network_projects = site.data.projects | where: "category", "networks" %}
{% assign nvidia_projects = site.data.projects | where: "category", "nvidia" %}
{% assign international_projects = site.data.projects | where: "category", "internationals" %}
{% assign other_projects = site.data.projects | where: "category", "others" %}

<section class="projects-page" id="projects">
  <div class="projects-hero">
    <p class="eyebrow">Portfolio 2020+</p>
    <h1>Research projects</h1>
    <p>
      Projects are organized by funding family and start year. Use the tabs to switch between
      FONDECYT, networks, NVIDIA, international collaborations, and other initiatives.
    </p>
    <p class="project-source">
      Source:
      <a href="https://postgrado.udec.cl/catalogo/academico/alexis-marcelo-salas-burgos" target="_blank" rel="noopener noreferrer">
        Catálogo Académico Postgrado UdeC
      </a>
      <span>· NVIDIA support retained from the lab site.</span>
    </p>
  </div>

  <div class="project-controls" aria-label="Project filters">
    <div class="control-block">
      <h2>Type</h2>
      <div class="project-tabs" role="tablist" aria-label="Project type tabs">
        <button class="project-tab active" type="button" role="tab" aria-selected="true" data-category="all">
          All <span>{{ total_projects }}</span>
        </button>
        <button class="project-tab" type="button" role="tab" aria-selected="false" data-category="fondecyt">
          FONDECYT <span>{{ fondecyt_projects | size }}</span>
        </button>
        <button class="project-tab" type="button" role="tab" aria-selected="false" data-category="networks">
          Networks <span>{{ network_projects | size }}</span>
        </button>
        <button class="project-tab" type="button" role="tab" aria-selected="false" data-category="nvidia">
          NVIDIA <span>{{ nvidia_projects | size }}</span>
        </button>
        <button class="project-tab" type="button" role="tab" aria-selected="false" data-category="internationals">
          Internationals <span>{{ international_projects | size }}</span>
        </button>
        <button class="project-tab" type="button" role="tab" aria-selected="false" data-category="others">
          Others <span>{{ other_projects | size }}</span>
        </button>
      </div>
    </div>

    <div class="control-block">
      <h2>Year</h2>
      <div class="year-filter-group" aria-label="Filter projects by start year">
        <button class="year-filter active" type="button" data-year="all" aria-pressed="true">
          All years <span>{{ total_projects }}</span>
        </button>
        {% for year_group in projects_by_year %}
          <button class="year-filter" type="button" data-year="{{ year_group.name }}" aria-pressed="false">
            {{ year_group.name }} <span>{{ year_group.items | size }}</span>
          </button>
        {% endfor %}
      </div>
    </div>
  </div>

  <p class="project-filter-status" aria-live="polite">
    Showing {{ total_projects }} projects from 2020 onward.
  </p>

  <div class="project-grid">
    {% for project in site.data.projects %}
      <article class="project-card" data-category="{{ project.category }}" data-year="{{ project.start_year }}">
        <div class="project-card-topline">
          <span class="project-category project-category-{{ project.category }}">{{ project.category_label }}</span>
          <span class="project-period">
            {{ project.start_year }}{% if project.end_year and project.end_year != project.start_year %}–{{ project.end_year }}{% endif %}
          </span>
        </div>

        <h2>{{ project.name }}</h2>

        <p class="project-description">{{ project.description }}</p>

        <dl class="project-details">
          {% if project.program %}
            <div>
              <dt>Program</dt>
              <dd>{{ project.program }}</dd>
            </div>
          {% endif %}
          {% if project.investigators %}
            <div>
              <dt>Investigators</dt>
              <dd>{{ project.investigators }}</dd>
            </div>
          {% endif %}
          {% if project.institution %}
            <div>
              <dt>Institution</dt>
              <dd>{{ project.institution }}</dd>
            </div>
          {% endif %}
          {% if project.role %}
            <div>
              <dt>Role</dt>
              <dd>{{ project.role }}</dd>
            </div>
          {% endif %}
          {% if project.status %}
            <div>
              <dt>Status</dt>
              <dd>{{ project.status }}</dd>
            </div>
          {% endif %}
        </dl>
      </article>
    {% endfor %}
  </div>
</section>

<style>
  .projects-page {
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

  .projects-hero {
    padding: 1.5rem;
    margin-bottom: 1.5rem;
    border: 1px solid var(--project-border);
    border-left: 6px solid var(--project-orange);
    border-radius: 16px;
    background: linear-gradient(135deg, #ffffff 0%, var(--project-bg) 100%);
  }

  .projects-hero .eyebrow {
    margin: 0 0 0.35rem;
    color: var(--project-orange);
    font-size: 0.78rem;
    font-weight: 800;
    letter-spacing: 0.08em;
    text-transform: uppercase;
  }

  .projects-hero h1 {
    margin: 0 0 0.6rem;
    color: var(--project-blue);
  }

  .projects-hero p {
    max-width: 820px;
    margin-bottom: 0.55rem;
    color: var(--project-ink);
  }

  .project-source {
    font-size: 0.92rem;
  }

  .project-source span {
    color: var(--project-muted);
  }

  .project-controls {
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

  .project-tabs,
  .year-filter-group {
    display: flex;
    flex-wrap: wrap;
    gap: 0.55rem;
  }

  .project-tab,
  .year-filter {
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

  .project-tab span,
  .year-filter span {
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

  .project-tab:hover,
  .project-tab:focus,
  .year-filter:hover,
  .year-filter:focus {
    border-color: var(--project-orange);
    transform: translateY(-1px);
  }

  .project-tab.active,
  .year-filter.active {
    border-color: var(--project-blue);
    background: var(--project-blue);
    color: #fff;
  }

  .project-tab.active span,
  .year-filter.active span {
    background: rgba(255, 255, 255, 0.18);
    color: #fff;
  }

  .project-filter-status {
    color: var(--project-muted);
    font-size: 0.92rem;
  }

  .project-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1rem;
  }

  .project-card {
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

  .project-card.is-hidden {
    display: none;
  }

  .project-card-topline {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: space-between;
    gap: 0.45rem;
  }

  .project-category,
  .project-period {
    border-radius: 999px;
    padding: 0.25rem 0.58rem;
    font-size: 0.72rem;
    font-weight: 800;
    letter-spacing: 0.01em;
  }

  .project-category {
    background: rgba(0, 60, 113, 0.1);
    color: var(--project-blue);
  }

  .project-category-fondecyt {
    background: rgba(230, 150, 53, 0.16);
    color: #8a4c0c;
  }

  .project-category-networks {
    background: rgba(53, 122, 56, 0.13);
    color: var(--project-green);
  }

  .project-category-nvidia {
    background: rgba(118, 185, 0, 0.16);
    color: #386100;
  }

  .project-category-internationals {
    background: rgba(107, 75, 184, 0.13);
    color: var(--project-purple);
  }

  .project-category-others {
    background: rgba(36, 41, 47, 0.1);
    color: var(--project-black);
  }

  .project-period {
    background: var(--project-bg);
    color: var(--project-muted);
  }

  .project-card h2 {
    margin: 0;
    color: var(--project-blue);
    font-size: 1.05rem;
    line-height: 1.35;
  }

  .project-description {
    margin: 0;
    color: var(--project-ink);
  }

  .project-details {
    display: grid;
    gap: 0.55rem;
    margin: auto 0 0;
  }

  .project-details div {
    padding-top: 0.55rem;
    border-top: 1px solid var(--project-border);
  }

  .project-details dt {
    color: var(--project-muted);
    font-size: 0.72rem;
    font-weight: 800;
    letter-spacing: 0.06em;
    text-transform: uppercase;
  }

  .project-details dd {
    margin: 0.15rem 0 0;
    color: var(--project-ink);
  }

  .project-empty-state {
    display: none;
    padding: 1rem;
    border: 1px dashed var(--project-border);
    border-radius: 14px;
    color: var(--project-muted);
    background: var(--project-bg);
  }

  .project-empty-state.is-visible {
    display: block;
  }

  @media (min-width: 780px) {
    .project-controls {
      grid-template-columns: 1.05fr 0.95fr;
    }
  }

  @media (max-width: 640px) {
    .projects-hero,
    .control-block {
      padding: 1rem;
    }

    .project-grid {
      grid-template-columns: 1fr;
    }
  }
</style>

<p class="project-empty-state" id="project-empty-state">No projects match this filter combination.</p>

<script>
  (function () {
    var tabs = Array.prototype.slice.call(document.querySelectorAll('.project-tab'));
    var yearButtons = Array.prototype.slice.call(document.querySelectorAll('.year-filter'));
    var cards = Array.prototype.slice.call(document.querySelectorAll('.project-card'));
    var status = document.querySelector('.project-filter-status');
    var emptyState = document.getElementById('project-empty-state');
    var total = {{ total_projects }};
    var activeCategory = 'all';
    var activeYear = 'all';

    function updateButtons(buttons, attr, value, selectedAttr) {
      buttons.forEach(function (button) {
        var isActive = button.getAttribute(attr) === value;
        button.classList.toggle('active', isActive);
        button.setAttribute(selectedAttr, isActive ? 'true' : 'false');
      });
    }

    function applyFilters() {
      var shown = 0;

      cards.forEach(function (card) {
        var categoryMatches = activeCategory === 'all' || card.getAttribute('data-category') === activeCategory;
        var yearMatches = activeYear === 'all' || card.getAttribute('data-year') === activeYear;
        var visible = categoryMatches && yearMatches;
        card.classList.toggle('is-hidden', !visible);
        if (visible) {
          shown += 1;
        }
      });

      updateButtons(tabs, 'data-category', activeCategory, 'aria-selected');
      updateButtons(yearButtons, 'data-year', activeYear, 'aria-pressed');

      if (status) {
        var typeLabel = activeCategory === 'all' ? 'all types' : activeCategory;
        var yearLabel = activeYear === 'all' ? 'all years' : activeYear;
        status.textContent = 'Showing ' + shown + ' of ' + total + ' projects · Type: ' + typeLabel + ' · Year: ' + yearLabel + '.';
      }

      if (emptyState) {
        emptyState.classList.toggle('is-visible', shown === 0);
      }
    }

    tabs.forEach(function (button) {
      button.addEventListener('click', function () {
        activeCategory = button.getAttribute('data-category');
        applyFilters();
      });
    });

    yearButtons.forEach(function (button) {
      button.addEventListener('click', function () {
        activeYear = button.getAttribute('data-year');
        applyFilters();
      });
    });
  })();
</script>
