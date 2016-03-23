---
layout: page
permalink: /gallery/
title: gallery
navbar: yes
description: Photography Gallery
---

{% for album in site.data.albums %}

<div class="project">
    <div class="thumbnail">
        <a href="/albums/{{ album.id }}">
        {% if album.cover %}
        <img class="thumbnail" src="{{ album.thumbfolder }}{{ album.cover }}"/>
        {% else %}
        <div class="thumbnail blankbox"></div>
        {% endif %}    
        <span>
            <h1>{{ album.title }}</h1>
            <br/>
            <p>{{ album.description }}</p>
        </span>
        </a>
    </div>
</div>

{% endfor %}
