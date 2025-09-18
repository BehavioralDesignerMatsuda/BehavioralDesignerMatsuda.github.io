---
title: "Talks & Presentations｜発表一覧"
permalink: /talks/
layout: single
author_profile: true
---

<p>
  Quick filter：
  <a href="/talks/international/">International</a> ｜ 
  <a href="/talks/domestic/">Domestic</a> ｜ 
  <a href="/talks/invited/">Invited</a> ｜ 
  <a href="/talks/symposium/">Symposium</a> ｜ 
  <a href="/talks/poster/">Poster</a>
</p>
<hr/>

<div class="entries-list">
{% assign items = site.talks | sort: "date" | reverse %}
{% for post in items %}
  {% include custom/archive-talk.html post=post %}
{% endfor %}
</div>
