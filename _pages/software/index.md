---
layout: page
title: Software
permalink: /software/
toggle: on
rank: 3
---

<div class="container">
    <div class="tab-nav">
        {% for category in site.categories %}
            <button class="{% if forloop.first %}active{% endif %}" data-tab-target="#{{ category.slug }}">{{ category.name }}</button>
        {% endfor %}
    </div>
    <div class="tab-content">
        {% for category in site.categories %}
            <div id="{{ category.slug }}" class="{% if forloop.first %}active{% endif %}">
                <h2>Category: {{ category.name }}</h2>
                <ul>
                    <li>Name: {{ category.software.name }}</li>
                    <li>Description: {{ category.software.description }}</li>
                    <li>Developers: {{ category.software.developers }}</li>
                    <li>Github: <a href="https://github.com/{{ category.software.github }}">github/{{ category.software.github }}</a></li>
                    <li>Version: {{ category.software.version }}</li>
                </ul>
            </div>
        {% endfor %}
    </div>
</div>

<style>
    /* Add a container to hold the tab navigation and content */
    .container {
        display: flex;
        flex-direction: row;
    }

    /* Style the tab navigation menu */
    .tab-nav {
        flex-basis: 200px; /* set the width of the tab navigation */
        background-color: #f0f0f0;
        border: 1px solid #ccc;
        padding: 20px;
        display: flex;
        flex-direction: column;
    }

    .tab-nav button {
        padding: 10px;
        border: none;
        background-color: #f0f0f0;
        cursor: pointer;
        width: 100%;
        border-bottom: 1px solid #ccc;
    }

    .tab-nav button:hover {
        background-color: #ccc;
    }

    .tab-nav button.active {
        background-color: #333;
        color: #fff;
    }

    /* Style the tab content */
    .tab-content {
        flex-grow: 1; /* make the content take up the remaining space */
        padding: 20px;
        border: 1px solid #ccc;
    }

    .tab-content div {
        display: none;
    }

    .tab-content div.active {
        display: block;
    }
</style>

<script>
    // Get the tab navigation buttons and content
    const tabNavButtons = document.querySelectorAll('.tab-nav button');
    const tabContentDivs = document.querySelectorAll('.tab-content div');

    // Add event listeners to the tab navigation buttons
    tabNavButtons.forEach(button => {
        button.addEventListener('click', () => {
            // Remove the active class from all buttons and content
            tabNavButtons.forEach(btn => btn.classList.remove('active'));
            tabContentDivs.forEach(div => div.classList.remove('active'));

            // Add the active class to the current button and content
            button.classList.add('active');
            const tabTarget = button.getAttribute('data-tab-target');
            document.querySelector(tabTarget).classList.add('active');
        });
    });
</script>

