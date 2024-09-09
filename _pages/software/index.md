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
                <button class="subcategory-button" data-description="{{ subcategory.description }}">{{ subcategory.name }}</button>
              </li>
            {% endfor %}
          </ul>
        </div>
      {% endif %}
    {% endfor %}
  </div>
  <div class="sidebar-box" id="sidebar-box">
    <h1><b>Welcome to Our Research Toolkit!</b></h1>

<p>Explore the suite of programs and tools we use to enhance our understanding of the world. Our resources include bioinformatics tools, drug information, chemical properties, and pharmaceutical data. These are integral to our research and findings. Use the navigation bar on the left to access the tools and information that support our scientific work.</p>
  </div>
</div>


<style>
    /* Global Styles */

    * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
    }

    body {
    font-family: Arial, sans-serif;
    }

    /* Container Styles */

    .container {
    display: flex;
    flex-direction: row;
    }

    /* Tab Navigation Styles */

    .tab-nav {
    flex-basis: 144px;
    background-color: #f0f0f0;
    padding: 10px;
    display: flex;
    flex-direction: column;
    font-size: 14px;
    }

    .tab-title {
    background-color: #aaa;
    cursor: pointer;
    width: 100%;
    font-weight: bold;
    font-size: 13px;
    padding-left: 10px;
    }

    /* Tab Content Styles */

    .tab-content {
    padding: 0px;
    border: 1px solid #ccc;
    font-size: 14px;
    }

    .tab-content ul {
    list-style: none;
    padding: 0;
    margin: 0;
    display: flex;
    flex-wrap: wrap;
    }

    .tab-content li {
    flex: 1;
    margin-bottom: 5px;
    }

    .tab-content li:first-child {
    margin-top: 10px;
    }

    .tab-content li:last-child {
    margin-bottom: 10px;
    }

    /* Subcategory Button Styles */

    .subcategory-button {
    background-color: #eee;
    border: none;
    padding: 5px 10px;
    font-size: 11px;
    cursor: pointer;
    width: 144px;
    }

    .subcategory-button:hover {
    background-color: #bbb;
    }

    /* Sidebar Box Styles */

    .sidebar-box {
    flex: 1;
    background-color: #fff;
    padding: 20px;
    padding-top: 5px;
    border: 1px solid #ddd;
    font-size: 15px;
    }
</style>

<script>
// Get the sidebar box element
const sidebarBox = document.getElementById('sidebar-box');

// Add event listener to subcategory buttons
document.querySelectorAll('.subcategory-button').forEach(button => {
  button.addEventListener('click', () => {
    const description = button.getAttribute('data-description');
    sidebarBox.innerHTML = `<p>${description}</p>`;
  });
});
</script>