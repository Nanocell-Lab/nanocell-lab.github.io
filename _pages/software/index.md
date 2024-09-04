---
layout: page
title: Software
permalink: /software/
toggle: on
rank: 3
---

<div class="software-wrapper">
  <ul class="software-category-list">
    {% for category in site.data.softwares | group_by: "category" %}
    <li>
        {{ category.grouper }}
        <ul>
            {% for software in category.items %} 
            <p>name: {{ software.name }}</p>
            <p>description: {{ software.description }}</p>
            <p>Developers: {{ software.developers }}</p>
            <p>Github: {{ software.github }}</p>
            <p>Version: {{ software.version }}</p>
            {% endfor %}
        </ul>
    </li>
    {% endfor %}
  </ul>
</div>


