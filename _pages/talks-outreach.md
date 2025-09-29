---
title: "Talks｜Outreach（一般・学校・企業）"
permalink: /talks/outreach/
layout: single
author_profile: true
date_label: "Presented"
---
<div class="entries-list">
{% assign items = site.talks | where: "format", "outreach" | sort: "date" | reverse %}
{% for post in items %}{% include archive-single.html %}{% endfor %}
</div>
