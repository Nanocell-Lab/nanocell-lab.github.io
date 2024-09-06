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
            <div class="tab-title">{{ software.category }}</div>
            <div id="tab-{{ forloop.index }}" class="tab-content">
                <ul>
                {% for subcategory in software.subcategories %}
                    <li class="subcategory-item">
                        <button class="subcategory-button" onclick="showDescription('{{ subcategory.description }}')">
                            {{ subcategory.name }}
                        </button>
                    </li>
                {% endfor %}
                </ul>
            </div>
        {% endif %}
        {% endfor %}
    </div>
    <div class="sidebar-box" id="sidebar-box">
        <p>This is a box at the right of the navigation tab.</p>
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
        flex-basis: 144px; /* set the width of the tab navigation */
        background-color: #f0f0f0;
        padding: 10px;
        display: flex;
        flex-direction: column;
        font-size: 14px; /* smaller font size */
    }

    /* Add styles for the tab-nav-text div */
    .tab-nav-text {
        position: absolute; /* position the text at the right side of the tab-nav */
        right: 10px; /* adjust the position to your liking */
        top: 10px; /* adjust the position to your liking */
        font-size: 14px; /* adjust the font size to your liking */
    }

    .tab-title {
        background-color: #aaa;
        cursor: pointer;
        width: 93%;
        font-weight: bold;
        font-size: 14px; /* smaller font size */
        padding-left: 10px; /* add a gap at the left of the word */
    }

    /* Style the tab content */
    .tab-content {
        padding: 0px;
        border: 1px solid #ccc;
        font-size: 14px; /* smaller font size */
    }

    .tab-content ul {
        list-style: none;
        padding: 0;
        margin: 0;
        display: flex; /* make the ul a flex container */
        flex-wrap: wrap; /* allow buttons to wrap to the next line */
    }

    .tab-content li {
        flex: 1; /* make each li take equal space */
        margin-bottom: 5px; /* add a gap between buttons */
    }

    .tab-content li:first-child {
        margin-top: 10px; /* remove the gap for the last button */
    }
    .tab-content li:last-child {
        margin-bottom: 10px; /* remove the gap for the last button */
    }

    /* Style the subcategory buttons */
    .subcategory-button {
        background-color: #ddd; /* grey background */
        border: none;
        padding: 10px 40px; /* make the button a bit larger */
        font-size: 10px;
        cursor: pointer;
        width: 144px; /* make the button take full width */
    }

    .description {
        padding: 10px 40px; /* make the button a bit larger */
        font-size: 5px;
        cursor: pointer;
        width: 144px; /* make the button take full width */
    }
    .subcategory-button:hover {
        background-color: #bbb; /* darker grey on hover */
    }

    /* Add styles for the subcategory item */
    .subcategory-item {
        display: flex; /* use flexbox layout */
        align-items: center; /* center the button and text vertically */
    }

    /* Add styles for the subcategory button */
    .subcategory-button {
        padding: 5px 10px; /* reduce the padding to make the buttons smaller */
        font-size: 12px; /* reduce the font size to make the buttons smaller */
        border: none; /* remove the border to make the buttons look cleaner */
        background-color: #f0f0f0; /* add a light gray background color */
        cursor: pointer; /* change the cursor to a pointing hand when hovering over the buttons */
    }

    /* Add styles for the sidebar box */
    .sidebar-box {
        flex: 1; /* take up the remaining space */
        background-color: #fff; /* white background */
        padding: 20px; /* add some padding */
        border: 1px solid #ddd; /* add a border */
        font-size: 15px;
    }
</style>

<script>
function showDescription(description) {
    var sidebarBox = document.getElementById('sidebar-box');
    sidebarBox.innerHTML = '<p>' + description + '</p>';
}
</script>