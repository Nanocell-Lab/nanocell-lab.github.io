---
layout: page
title: Projects
permalink: /projects/
toggle: on
rank: 1
---

<div class="lab-wrapper">
    <ul class="lab-list">
    {% for project in site.data.projects %}
    {% if project.name and project.description %}
        <li>
            <h2>{{ project.name }}</h2>
            {% if project.photo %}
                <img class="float-right projects-photo" src="{{ project.photo | prepend: site.images_dir | prepend: site.baseurl }}">
            {% endif %}
            {% if project.funding %}
                <p><b>Funding: </b>{{ project.funding }}</p>
            {% endif %}
            {% if project.collaborators %}
                <p><b>Collaborators: </b>{{ project.collaborators }}</p>
            {% endif %}
            {% if project.assignees %}
                <p><b>Assignees: </b>{{ project.assignees }}</p>
            {% endif %}
            <p>{{ project.description }}</p>
        </li>
    {% endif %}
    {% endfor %}
    {% for project in site.data.projects %}
    {% if project.title and project.list %}
        <li>
            <h1>{{ project.title }}</h1>
            {% if project.list %}
                <p>{{ project.list1 }}</p>
                <p>{{ project.list2 }}</p>
                <p>{{ project.list3 }}</p>
                <p>{{ project.list4 }}</p>
            {% endif %}
    {% endif %}
    {% endfor %}
    </ul>
</div>
