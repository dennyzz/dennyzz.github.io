---
layout: page
permalink: /photography/
title: Photography
navbar: yes
description: 
---

{% for album in site.data.albums %}

<div class="project">
    <div class="thumbnail">
        <a href="{{ site.baseurl }}/photography/albums/{{ album.id }}">
        {% if album.cover %}
        <img class="thumbnail" src="{{ album.rootfolder }}{{ album.thumbfolder }}{{ album.cover }}"/>
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
