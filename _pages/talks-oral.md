---
title: "Talks｜Oral（口頭）"
permalink: /talks/oral/
layout: single
author_profile: true
date_label: "Presented"
---
<div class="entries-list">
{% assign items = site.talks | where: "format", "oral" | sort: "date" | reverse %}
{% for post in items %}
  {% include archive-single-presentation.html %}
{% endfor %}
</div>
