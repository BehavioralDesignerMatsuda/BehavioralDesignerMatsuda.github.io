---
title: "Publications｜論文"
permalink: /publications/
layout: single
author_profile: true
---

<div class="entries-list">
{% assign pubs = site.publications | sort: "date" | reverse %}
{% for post in pubs %}
  {% include archive-single.html %}
{% endfor %}
</div>
