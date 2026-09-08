---
layout: page
title: Presentations
permalink: /presentations/
toggle: on
rank: 6
---

{% assign presentations_by_year = site.data.presentations | group_by: "year" | sort: "name" | reverse %}
{% assign total_presentations = site.data.presentations | size %}

<section class="presentations-page" id="presentations">
  <div class="presentations-hero">
    <p class="eyebrow">Conference activity</p>
    <h1>Conference Presentations</h1>
    <p>
      Conference talks, posters, abstracts, and invited presentations connected to the laboratory's work in molecular dynamics,
      oncology, bioinformatics, territorial science, and open science.
    </p>
  </div>

  <div class="presentation-toolbar" aria-label="Filter presentations by year">
    <button class="year-filter active" type="button" data-year="all" aria-pressed="true">
      All <span>{{ total_presentations }}</span>
    </button>
    {% for year_group in presentations_by_year %}
      <button class="year-filter" type="button" data-year="{{ year_group.name }}" aria-pressed="false">
        {{ year_group.name }} <span>{{ year_group.items | size }}</span>
      </button>
    {% endfor %}
  </div>

  <p class="presentation-filter-status" aria-live="polite">
    Showing {{ total_presentations }} conference presentations.
  </p>

  <div class="presentation-year-groups">
    {% for year_group in presentations_by_year %}
      <section class="presentation-year-group" data-year-group="{{ year_group.name }}">
        <div class="year-heading">
          <h2>{{ year_group.name }}</h2>
          <span>{{ year_group.items | size }} presentations</span>
        </div>

        <div class="presentation-grid">
          {% for presentation in year_group.items %}
            <article class="presentation-card" data-year="{{ presentation.year }}">
              <div class="presentation-card-header">
                <span class="presentation-year">{{ presentation.year }}</span>
                <span class="presentation-date">{{ presentation.date_label }}</span>
              </div>

              <h3>
                {% if presentation.url %}
                  <a href="{{ presentation.url }}" target="_blank" rel="noopener noreferrer">{{ presentation.title }}</a>
                {% else %}
                  {{ presentation.title }}
                {% endif %}
              </h3>

              <dl class="presentation-details">
                <div>
                  <dt>Presenters</dt>
                  <dd>{{ presentation.presenters }}</dd>
                </div>
                <div>
                  <dt>Conference / event</dt>
                  <dd>{{ presentation.event }}</dd>
                </div>
              </dl>
            </article>
          {% endfor %}
        </div>
      </section>
    {% endfor %}
  </div>
</section>

<style>
  .presentations-page {
    --presentation-blue: #003c71;
    --presentation-orange: #e69635;
    --presentation-ink: #243447;
    --presentation-muted: #687386;
    --presentation-border: #dfe7f0;
    --presentation-bg: #f7fafc;
  }

  .presentations-hero {
    padding: 1.5rem;
    margin-bottom: 1.5rem;
    border: 1px solid var(--presentation-border);
    border-left: 6px solid var(--presentation-orange);
    border-radius: 16px;
    background: linear-gradient(135deg, #ffffff 0%, var(--presentation-bg) 100%);
  }

  .presentations-hero .eyebrow {
    margin: 0 0 0.35rem;
    color: var(--presentation-orange);
    font-size: 0.78rem;
    font-weight: 800;
    letter-spacing: 0.08em;
    text-transform: uppercase;
  }

  .presentations-hero h1 {
    margin: 0 0 0.6rem;
    color: var(--presentation-blue);
  }

  .presentations-hero p {
    max-width: 820px;
    margin-bottom: 0;
    color: var(--presentation-ink);
  }

  .presentation-toolbar {
    display: flex;
    flex-wrap: wrap;
    gap: 0.55rem;
    margin: 0 0 0.75rem;
  }

  .year-filter {
    cursor: pointer;
    border: 1px solid var(--presentation-border);
    border-radius: 999px;
    padding: 0.55rem 0.9rem;
    background: #fff;
    color: var(--presentation-blue);
    font-weight: 800;
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
    background: var(--presentation-bg);
    color: var(--presentation-muted);
    font-size: 0.78rem;
  }

  .year-filter:hover,
  .year-filter:focus {
    border-color: var(--presentation-orange);
    transform: translateY(-1px);
  }

  .year-filter.active {
    border-color: var(--presentation-blue);
    background: var(--presentation-blue);
    color: #fff;
  }

  .year-filter.active span {
    background: rgba(255, 255, 255, 0.18);
    color: #fff;
  }

  .presentation-filter-status {
    color: var(--presentation-muted);
    font-size: 0.92rem;
  }

  .presentation-year-group {
    margin-top: 2rem;
  }

  .presentation-year-group.is-hidden {
    display: none;
  }

  .year-heading {
    display: flex;
    align-items: baseline;
    justify-content: space-between;
    gap: 1rem;
    margin-bottom: 0.85rem;
    border-bottom: 2px solid var(--presentation-border);
  }

  .year-heading h2 {
    margin-bottom: 0.35rem;
    color: var(--presentation-blue);
  }

  .year-heading span {
    color: var(--presentation-muted);
    font-size: 0.9rem;
    white-space: nowrap;
  }

  .presentation-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1rem;
  }

  .presentation-card {
    display: flex;
    flex-direction: column;
    gap: 0.85rem;
    min-height: 100%;
    padding: 1rem;
    border: 1px solid var(--presentation-border);
    border-top: 4px solid var(--presentation-orange);
    border-radius: 14px;
    background: #fff;
    box-shadow: 0 8px 22px rgba(0, 60, 113, 0.07);
  }

  .presentation-card-header {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    gap: 0.45rem;
  }

  .presentation-year,
  .presentation-date {
    border-radius: 999px;
    padding: 0.25rem 0.58rem;
    font-size: 0.72rem;
    font-weight: 800;
    letter-spacing: 0.01em;
  }

  .presentation-year {
    background: rgba(0, 60, 113, 0.1);
    color: var(--presentation-blue);
  }

  .presentation-date {
    background: var(--presentation-bg);
    color: var(--presentation-muted);
  }

  .presentation-card h3 {
    margin: 0;
    color: var(--presentation-blue);
    font-size: 1.02rem;
    line-height: 1.35;
  }

  .presentation-card h3 a {
    color: var(--presentation-blue);
  }

  .presentation-details {
    display: grid;
    gap: 0.55rem;
    margin: auto 0 0;
  }

  .presentation-details div {
    padding-top: 0.55rem;
    border-top: 1px solid var(--presentation-border);
  }

  .presentation-details dt {
    color: var(--presentation-muted);
    font-size: 0.72rem;
    font-weight: 800;
    letter-spacing: 0.06em;
    text-transform: uppercase;
  }

  .presentation-details dd {
    margin: 0.15rem 0 0;
    color: var(--presentation-ink);
  }

  @media (max-width: 640px) {
    .presentations-hero {
      padding: 1rem;
    }

    .year-heading {
      display: block;
    }

    .presentation-grid {
      grid-template-columns: 1fr;
    }
  }
</style>

<script>
  (function () {
    var buttons = Array.prototype.slice.call(document.querySelectorAll('.year-filter'));
    var groups = Array.prototype.slice.call(document.querySelectorAll('.presentation-year-group'));
    var status = document.querySelector('.presentation-filter-status');
    var total = {{ total_presentations }};

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
          shown += group.querySelectorAll('.presentation-card').length;
        }
      });

      if (status) {
        status.textContent = year === 'all'
          ? 'Showing ' + total + ' conference presentations.'
          : 'Showing ' + shown + ' conference presentations from ' + year + '.';
      }
    }

    buttons.forEach(function (button) {
      button.addEventListener('click', function () {
        setYear(button.getAttribute('data-year'));
      });
    });
  })();
</script>
