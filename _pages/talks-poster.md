---
title: "Talks｜Poster"
permalink: /talks/poster/
layout: single
author_profile: true
date_label: "Presented"
---
<div class="entries-list">
{% assign items = site.talks | where: "format", "poster" | sort: "date" | reverse %}
{% for post in items %}
  {% include archive-single-presentation.html %}
{% endfor %}
</div>
