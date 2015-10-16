---
layout: post
title: "Index"
permalink: /index/
date: 2015-10-15 18:21:13
---
# The index of articles
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>

