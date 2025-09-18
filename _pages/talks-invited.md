---
title: "Talks｜Invited"
permalink: /talks/invited/
layout: single
author_profile: true
---
<div class="entries-list">
{% assign items = site.talks | where: "format", "invited" | sort: "date" | reverse %}
{% for post in items %}
  {% include custom/archive-talk.html post=post %}
{% endfor %}
</div>
