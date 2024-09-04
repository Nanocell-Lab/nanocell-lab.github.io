---
layout: page
title: Software
permalink: /software/
toggle: on
rank: 3
---

<div class="software-wrapper">
  <ul class="software-category-list">
    {% for software in site.data.softwares %}
      {% if software.category %}
        <div class="box">
          <h2>{{ software.category }}</h2>
          <ul>
            <li><strong>Name:</strong> {{ software.name }}</li>
            <li><strong>Description:</strong> {{ software.description }}</li>
            <li><strong>Developers:</strong> {{ software.developers }}</li>
            <li><strong>GitHub:</strong> {{ software.github }}</li>
            <li><strong>Version:</strong> {{ software.version }}</li>
          </ul>
        </div>
      {% endif %}
    {% endfor %}
  </ul>
</div>



