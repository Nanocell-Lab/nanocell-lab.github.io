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
    </ul>
</div>


<div class="lab-wrapper">
    <ul class="lab-list">
    {% for project in site.data.projects %}
        {% if project.support %}
            <li class="small-text">
                <h2><strong>{{ project.support }}</strong></h2>
                <p>{{ project.acknowledge }}</p>
                <ul>
                {% for donation in project.donations %}
                    <li class="small-text">
                        <h4>{{ donation.year }}</h4>
                        <strong>Hardware Donation:</strong> {{ donation.donation }}<br>
                        <strong>Impact:</strong> {{ donation.impact }}
                    </li>
                {% endfor %}
                </ul> <!-- Close the donations list -->
                <ul>
                {% for activity in project.activities %}
                    <li class="small-text">
                        <h4>{{ activity.year }}</h4> <!-- Use activity.year instead of donation.year -->
                        <strong>Activities:</strong> {{ activity.activity }}<br> <!-- Use activity.description instead of donation.activity -->
                        <strong>Impact:</strong> {{ activity.impact }} <!-- Use activity.impact instead of donation.impact -->
                    </li>
                {% endfor %}
                </ul> <!-- Close the activities list -->
            </li>
        {% endif %}
    {% endfor %}
    </ul>
</div>


<style>
    .small-text {
        font-size: 0.95em; /* Adjust the value to make the text smaller or larger */
    }

    .lab-list {
        padding-top: 10px; /* Ensure units are specified for padding */
        margin: 0; /* Remove margin from the list */
    }

    .lab-list h4 {
        margin-bottom: 0; /* Remove bottom margin to reduce space */
        margin-top: 0; /* Remove top margin to reduce space */
    }

    .lab-list ul {
        padding-left: 30px; /* Adjust indentation for nested lists if needed */
    }
</style>