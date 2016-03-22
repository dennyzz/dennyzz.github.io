---
layout: page
title: projectss
permalink: /projectss
navbar: yes
description: 
---

{% for projects in site.projects %}

{% if projects.redirect %}
<div class="projects">
    <div class="thumbnail">
        <a href="{{ projects.redirect }}" target="_blank">
        {% if projects.img %}
        <img class="thumbnail" src="{{ projects.img }}"/>
        {% else %}
        <div class="thumbnail blankbox"></div>
        {% endif %}    
        <span>
            <h1>{{ projects.title }}</h1>
            <br/>
            <p>{{ projects.description }}</p>
        </span>
        </a>
    </div>
</div>
{% else %}

<div class="projects ">
    <div class="thumbnail">
        <a href="{{ site.baseurl }}{{ projects.url }}">
        {% if projects.img %}
        <img class="thumbnail" src="{{ projects.img }}"/>
        {% else %}
        <div class="thumbnail blankbox"></div>
        {% endif %}    
        <span>
            <h1>{{ projects.title }}</h1>
            <br/>
            <p>{{ projects.description }}</p>
        </span>
        </a>
    </div>
</div>

{% endif %}

{% endfor %}
