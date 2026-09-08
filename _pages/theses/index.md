---
layout: page
title: Theses
permalink: /theses/
toggle: on
rank: 5
---

{% assign theses_by_year = site.data.theses | group_by: "year" | sort: "name" | reverse %}
{% assign total_theses = site.data.theses | size %}
{% assign undergraduate_theses = site.data.theses | where: "level", "undergraduate" %}
{% assign postgraduate_theses = site.data.theses | where: "level", "postgraduate" %}

<section class="theses-page" id="theses">
  <div class="theses-hero">
    <p class="eyebrow">Supervised theses</p>
    <h1>Theses Directed</h1>
    <p>
      Undergraduate and postgraduate theses supervised by Alexis Salas Burgos, organized by academic level and year.
    </p>
  </div>

  <div class="theses-controls" aria-label="Thesis filters">
    <div class="control-block">
      <h2>Academic level</h2>
      <div class="thesis-tabs" role="tablist" aria-label="Filter theses by academic level">
        <button class="thesis-tab active" type="button" role="tab" aria-selected="true" data-level="all">
          All <span>{{ total_theses }}</span>
        </button>
        <button class="thesis-tab" type="button" role="tab" aria-selected="false" data-level="undergraduate">
          Undergraduate <span>{{ undergraduate_theses | size }}</span>
        </button>
        <button class="thesis-tab" type="button" role="tab" aria-selected="false" data-level="postgraduate">
          Postgraduate <span>{{ postgraduate_theses | size }}</span>
        </button>
      </div>
    </div>

    <div class="control-block">
      <h2>Year</h2>
      <div class="year-filter-group" aria-label="Filter theses by year">
        <button class="year-filter active" type="button" data-year="all" aria-pressed="true">
          All years <span>{{ total_theses }}</span>
        </button>
        {% for year_group in theses_by_year %}
          <button class="year-filter" type="button" data-year="{{ year_group.name }}" aria-pressed="false">
            {{ year_group.name }} <span>{{ year_group.items | size }}</span>
          </button>
        {% endfor %}
      </div>
    </div>
  </div>

  <p class="thesis-filter-status" aria-live="polite">
    Showing {{ total_theses }} supervised theses.
  </p>

  <div class="thesis-grid">
    {% for thesis in site.data.theses %}
      <article class="thesis-card" data-level="{{ thesis.level }}" data-year="{{ thesis.year }}">
        <div class="thesis-card-topline">
          <span class="thesis-level thesis-level-{{ thesis.level }}">{{ thesis.level_label }}</span>
          <span class="thesis-year">{{ thesis.year }}</span>
        </div>

        <h2>{{ thesis.title }}</h2>

        <dl class="thesis-details">
          <div>
            <dt>Student</dt>
            <dd>{{ thesis.student }}</dd>
          </div>
          <div>
            <dt>Advisor{% if thesis.advisors contains ";" %}s{% endif %}</dt>
            <dd>{{ thesis.advisors }}</dd>
          </div>
          <div>
            <dt>Degree</dt>
            <dd>{{ thesis.degree }}</dd>
          </div>
          <div>
            <dt>Institution</dt>
            <dd>{{ thesis.institution }}</dd>
          </div>
        </dl>
      </article>
    {% endfor %}
  </div>

  <p class="thesis-empty-state" id="thesis-empty-state">No theses match this filter combination.</p>
</section>

<style>
  .theses-page {
    --thesis-blue: #003c71;
    --thesis-orange: #e69635;
    --thesis-ink: #243447;
    --thesis-muted: #687386;
    --thesis-border: #dfe7f0;
    --thesis-bg: #f7fafc;
    --thesis-green: #357a38;
    --thesis-purple: #6b4bb8;
  }

  .theses-hero {
    padding: 1.5rem;
    margin-bottom: 1.5rem;
    border: 1px solid var(--thesis-border);
    border-left: 6px solid var(--thesis-orange);
    border-radius: 16px;
    background: linear-gradient(135deg, #ffffff 0%, var(--thesis-bg) 100%);
  }

  .theses-hero .eyebrow {
    margin: 0 0 0.35rem;
    color: var(--thesis-orange);
    font-size: 0.78rem;
    font-weight: 800;
    letter-spacing: 0.08em;
    text-transform: uppercase;
  }

  .theses-hero h1 {
    margin: 0 0 0.6rem;
    color: var(--thesis-blue);
  }

  .theses-hero p {
    max-width: 760px;
    margin-bottom: 0;
    color: var(--thesis-ink);
  }

  .theses-controls {
    display: grid;
    grid-template-columns: 1fr;
    gap: 1rem;
    margin-bottom: 0.85rem;
  }

  .control-block {
    padding: 1rem;
    border: 1px solid var(--thesis-border);
    border-radius: 14px;
    background: #fff;
  }

  .control-block h2 {
    margin: 0 0 0.75rem;
    color: var(--thesis-blue);
    font-size: 1rem;
  }

  .thesis-tabs,
  .year-filter-group {
    display: flex;
    flex-wrap: wrap;
    gap: 0.55rem;
  }

  .thesis-tab,
  .year-filter {
    cursor: pointer;
    border: 1px solid var(--thesis-border);
    border-radius: 999px;
    padding: 0.55rem 0.9rem;
    background: #fff;
    color: var(--thesis-blue);
    font-weight: 800;
    line-height: 1;
    transition: background 0.18s ease, border-color 0.18s ease, color 0.18s ease, transform 0.18s ease;
  }

  .thesis-tab span,
  .year-filter span {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    min-width: 1.35rem;
    margin-left: 0.35rem;
    padding: 0.18rem 0.35rem;
    border-radius: 999px;
    background: var(--thesis-bg);
    color: var(--thesis-muted);
    font-size: 0.78rem;
  }

  .thesis-tab:hover,
  .thesis-tab:focus,
  .year-filter:hover,
  .year-filter:focus {
    border-color: var(--thesis-orange);
    transform: translateY(-1px);
  }

  .thesis-tab.active,
  .year-filter.active {
    border-color: var(--thesis-blue);
    background: var(--thesis-blue);
    color: #fff;
  }

  .thesis-tab.active span,
  .year-filter.active span {
    background: rgba(255, 255, 255, 0.18);
    color: #fff;
  }

  .thesis-filter-status {
    color: var(--thesis-muted);
    font-size: 0.92rem;
  }

  .thesis-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1rem;
  }

  .thesis-card {
    display: flex;
    flex-direction: column;
    gap: 0.85rem;
    min-height: 100%;
    padding: 1rem;
    border: 1px solid var(--thesis-border);
    border-top: 4px solid var(--thesis-orange);
    border-radius: 14px;
    background: #fff;
    box-shadow: 0 8px 22px rgba(0, 60, 113, 0.07);
  }

  .thesis-card.is-hidden {
    display: none;
  }

  .thesis-card-topline {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    gap: 0.45rem;
  }

  .thesis-level,
  .thesis-year {
    border-radius: 999px;
    padding: 0.25rem 0.58rem;
    font-size: 0.72rem;
    font-weight: 800;
    letter-spacing: 0.01em;
  }

  .thesis-level-undergraduate {
    background: rgba(53, 122, 56, 0.13);
    color: var(--thesis-green);
  }

  .thesis-level-postgraduate {
    background: rgba(107, 75, 184, 0.13);
    color: var(--thesis-purple);
  }

  .thesis-year {
    background: var(--thesis-bg);
    color: var(--thesis-muted);
  }

  .thesis-card h2 {
    margin: 0;
    color: var(--thesis-blue);
    font-size: 1.05rem;
    line-height: 1.35;
  }

  .thesis-details {
    display: grid;
    gap: 0.55rem;
    margin: auto 0 0;
  }

  .thesis-details div {
    padding-top: 0.55rem;
    border-top: 1px solid var(--thesis-border);
  }

  .thesis-details dt {
    color: var(--thesis-muted);
    font-size: 0.72rem;
    font-weight: 800;
    letter-spacing: 0.06em;
    text-transform: uppercase;
  }

  .thesis-details dd {
    margin: 0.15rem 0 0;
    color: var(--thesis-ink);
  }

  .thesis-empty-state {
    display: none;
    margin-top: 1rem;
    padding: 1rem;
    border: 1px dashed var(--thesis-border);
    border-radius: 14px;
    color: var(--thesis-muted);
    background: var(--thesis-bg);
  }

  .thesis-empty-state.is-visible {
    display: block;
  }

  @media (min-width: 780px) {
    .theses-controls {
      grid-template-columns: 0.8fr 1.2fr;
    }
  }

  @media (max-width: 640px) {
    .theses-hero,
    .control-block {
      padding: 1rem;
    }

    .thesis-grid {
      grid-template-columns: 1fr;
    }
  }
</style>

<script>
  (function () {
    var tabs = Array.prototype.slice.call(document.querySelectorAll('.thesis-tab'));
    var yearButtons = Array.prototype.slice.call(document.querySelectorAll('.year-filter'));
    var cards = Array.prototype.slice.call(document.querySelectorAll('.thesis-card'));
    var status = document.querySelector('.thesis-filter-status');
    var emptyState = document.getElementById('thesis-empty-state');
    var total = {{ total_theses }};
    var activeLevel = 'all';
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
        var levelMatches = activeLevel === 'all' || card.getAttribute('data-level') === activeLevel;
        var yearMatches = activeYear === 'all' || card.getAttribute('data-year') === activeYear;
        var visible = levelMatches && yearMatches;
        card.classList.toggle('is-hidden', !visible);
        if (visible) {
          shown += 1;
        }
      });

      updateButtons(tabs, 'data-level', activeLevel, 'aria-selected');
      updateButtons(yearButtons, 'data-year', activeYear, 'aria-pressed');

      if (status) {
        var levelLabel = activeLevel === 'all' ? 'all levels' : activeLevel;
        var yearLabel = activeYear === 'all' ? 'all years' : activeYear;
        status.textContent = 'Showing ' + shown + ' of ' + total + ' theses · Level: ' + levelLabel + ' · Year: ' + yearLabel + '.';
      }

      if (emptyState) {
        emptyState.classList.toggle('is-visible', shown === 0);
      }
    }

    tabs.forEach(function (button) {
      button.addEventListener('click', function () {
        activeLevel = button.getAttribute('data-level');
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
