---
layout: page
permalink: /gallery
title: gallery
navbar: yes
description: 
---

<ul class="post-list">
{% for album in site.gallery %}
    <li>
        <h2><a class="poem-title" href="{{ poem.url | prepend: site.baseurl }}">{{ album.title }}</a></h2>
        <p class="post-meta">{{ album.date | date: '%B %-d, %Y — %H:%M' }}</p>
      </li>
{% endfor %}
</ul>