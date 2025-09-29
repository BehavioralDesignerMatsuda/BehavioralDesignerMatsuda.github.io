---
title: "Talks｜International"
permalink: /talks/international/
layout: single
author_profile: true
date_label: "Presented"
---
<div class="entries-list">
{% assign items = site.talks | where: "audience", "international" | sort: "date" | reverse %}
{% for post in items %}
  {% include custom/archive-talk.html post=post %}
{% endfor %}
</div>
