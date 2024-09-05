---
layout: page
title: Software
permalink: /software/
toggle: on
rank: 3
---

<div class="container">
    <div class="tab-nav">
    {% for software in site.data.softwares %}
    {% if software.category %}
            <button class="active" data-tab-target="#tab-{{ loop.index }}">{{ software.category }}</button>
                <div class="tab-content">
                    <div id="tab1" class="active">
                        <h2>Category: Categoria de prueba</h2>
                        <ul>
                            <li>Name: nombre de prueba</li>
                            <li>Description: de prueba</li>
                            <li>Developers: los probadores</li>
                            <li>Github: <a href="https://github.com/prueba">github/prueba</a></li>
                            <li>Version: version de prueba</li>
                        </ul>
                    </div>
                </div>
    {% endif %}
    {% endfor %}
    </div>
    <div class="tab-content">
        <div id="tab1" class="active">
            <h2>Category: Categoria de prueba</h2>
            <ul>
                <li>Name: nombre de prueba</li>
                <li>Description: de prueba</li>
                <li>Developers: los probadores</li>
                <li>Github: <a href="https://github.com/prueba">github/prueba</a></li>
                <li>Version: version de prueba</li>
            </ul>
        </div>
        <div id="tab2">
            <h2>Category: Categoria de p2rueba</h2>
            <ul>
                <li>Name: nombre de prueba 2</li>
                <li>Description: de prueba2</li>
                <li>Developers: los probado2res</li>
                <li>Github: <a href="https://github.com/prueb2a">github/prueb2a</a></li>
                <li>Version: version de prueba2</li>
            </ul>
        </div>
        <div id="tab3">
            <h2>Category: Categoria de prueba3</h2>
            <ul>
                <li>Name: nombre de prue3ba</li>
                <li>Description: de prueb3a</li>
                <li>Developers: los probadores3</li>
                <li>Github: <a href="https://github.com/prueba3">github/prueba3</a></li>
                <li>Version: version de pr3ueba</li>
            </ul>
        </div>
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
    const tabNavContainer = document.querySelector('.tab-nav');

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

            // Create a new button and append it to the tab navigation container
            const newButton = document.createElement('button');
            newButton.textContent = 'New Button';
            newButton.addEventListener('click', () => {
                console.log('New button clicked!');
            });
            tabNavContainer.appendChild(newButton);
        });
    });
</script>
