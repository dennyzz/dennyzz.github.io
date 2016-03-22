---
layout: page
permalink: /gallery
title: Gallery
navbar: yes
description: 
---

<ul class="post-list">
{% for album in site.gallery %}
    <li>
        <h2><a class="poem-title" href="{{ poem.url | prepend: site.baseurl }}">{{ portfolio.title }}</a></h2>
        <p class="post-meta">{{ portfolio.date | date: '%B %-d, %Y — %H:%M' }}</p>
      </li>
{% endfor %}
</ul>