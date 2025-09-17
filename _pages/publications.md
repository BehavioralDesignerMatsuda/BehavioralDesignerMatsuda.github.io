---
title: "Publications｜論文"
permalink: /publications/
layout: single
author_profile: true
---

<p><strong>Debug:</strong> site.publications size = {{ site.publications | size }}</p>

<ul>
{% for post in site.publications %}
  <li>{{ post.date | date: "%Y-%m-%d" }} — <a href="{{ post.url | relative_url }}">{{ post.title }}</a></li>
{% endfor %}
</ul>
