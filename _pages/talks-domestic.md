---
title: "Talks｜Domestic（国内）"
permalink: /talks/domestic/
layout: single
author_profile: true
---
<div class="entries-list">
{% assign items = site.talks | where: "audience", "domestic" | sort: "date" | reverse %}
{% for post in items %}
  {% include archive-single.html %}
{% endfor %}
</div>
