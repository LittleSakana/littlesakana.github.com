---
layout: archive
title: "其他"
date: 2014-05-30T11:39:03-04:00
modified:
excerpt: "杂七杂八的东西"
tags: []
image:
  feature:
  teaser:
---

<div class="tiles">
{% for post in site.categories.git %}
  {% include post-grid.html %}
{% endfor %}
</div><!-- /.tiles -->