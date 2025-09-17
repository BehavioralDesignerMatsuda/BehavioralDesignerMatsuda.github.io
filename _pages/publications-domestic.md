---
title: "Publications｜Domestic (Japanese)"
permalink: /publications/domestic/
layout: single
author_profile: true
---
<div class="entries-list">
{% assign pubs = site.publications | where: "category", "domestic" | sort: "date" | reverse %}
{% for post in pubs %}
  {% include archive-single.html %}
{% endfor %}
</div>
