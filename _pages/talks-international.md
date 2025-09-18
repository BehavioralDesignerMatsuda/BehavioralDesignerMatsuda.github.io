---
title: "Talks｜International"
permalink: /talks/international/
layout: single
author_profile: true
---
<div class="entries-list">
{% assign items = site.talks | where: "audience", "international" | sort: "date" | reverse %}
{% for post in items %}
  {% include archive-single.html %}
{% endfor %}
</div>
