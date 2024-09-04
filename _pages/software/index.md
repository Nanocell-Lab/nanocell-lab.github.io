---
layout: page
title: Software
permalink: /software/
toggle: on
rank: 3
---

<div class="container">
    <div class="tab-nav">
        <button class="active" data-tab-target="#tab1">Tab 1</button>
        <button data-tab-target="#tab2">Tab 2</button>
        <button data-tab-target="#tab3">Tab 3</button>
    </div>
    <div class="tab-content">
        <div id="tab1" class="active">
            <h2>Tab 1 Content</h2>
            <p>This is the content of Tab 1.</p>
        </div>
        <div id="tab2">
            <h2>Tab 2 Content</h2>
            <p>This is the content of Tab 2.</p>
        </div>
        <div id="tab3">
            <h2>Tab 3 Content</h2>
            <p>This is the content of Tab 3.</p>
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

