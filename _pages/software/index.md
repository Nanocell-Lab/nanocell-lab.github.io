---
layout: page
title: Software
permalink: /software/
toggle: on
rank: 3
---

<div class="software-list">
  {% for software in site.data.software %}
    <div class="box">
      <p id="initial-text-{{ software.name }}">{{ software.name }}</p>
      <p id="hidden-text-{{ software.name }}" style="display: none;">
        {{ software.description }}<br>
        Developed by: {{ software.developers }}<br>
        GitHub: {{ software.github }}<br>
        Version: {{ software.version }}
      </p>
    </div>
  {% endfor %}
</div>


