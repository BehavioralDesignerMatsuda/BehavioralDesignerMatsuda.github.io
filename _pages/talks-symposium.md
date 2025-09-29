---
title: "Talks｜Symposium"
permalink: /talks/symposium/
layout: single
author_profile: true
date_label: "Presented"
---
<div class="entries-list">
{% assign items = site.talks | where: "format", "symposium" | sort: "date" | reverse %}
{% for post in items %}
  {% include archive-single-presentation.html %}
{% endfor %}
</div>
