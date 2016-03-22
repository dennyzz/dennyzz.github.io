---
layout: page
permalink: /portfolio
title: portfolio
navbar: yes
description: 
---

<ul class="post-list">
{% for portfolio in site.portfolio reversed %}
    <li>
        <h2><a class="poem-title" href="{{ poem.url | prepend: site.baseurl }}">{{ portfolio.title }}</a></h2>
        <p class="post-meta">{{ portfolio.date | date: '%B %-d, %Y — %H:%M' }}</p>
      </li>
{% endfor %}
</ul>