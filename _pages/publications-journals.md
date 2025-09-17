---
title: "Publications｜Journals"
permalink: /publications/journals/
layout: single
author_profile: true
---
<div class="entries-list">
{% assign pubs = site.publications | where: "category", "journals" | sort: "date" | reverse %}
{% for post in pubs %}
  {% include archive-single.html %}
{% endfor %}
</div>
