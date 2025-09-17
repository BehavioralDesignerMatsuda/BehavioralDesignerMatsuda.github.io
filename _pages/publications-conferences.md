---
title: "Publications｜Conferences"
permalink: /publications/conferences/
layout: single
author_profile: true
---
<div class="entries-list">
{% assign pubs = site.publications | where: "category", "conferences" | sort: "date" | reverse %}
{% for post in pubs %}
  {% include archive-single.html %}
{% endfor %}
</div>
