---
title: "Talks｜Oral（口頭）"
permalink: /talks/oral/
layout: single
author_profile: true
---
<div class="entries-list">
{% assign items = site.talks | where: "format", "oral" | sort: "date" | reverse %}
{% for post in items %}
  {% include custom/archive-talk.html post=post %}
{% endfor %}
</div>
