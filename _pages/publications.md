---
title: "Publications｜論文"
permalink: /publications/
layout: single
author_profile: true
---

<p>
  <a href="/publications/journals/">Journals（英語・査読）</a> ｜ 
  <a href="/publications/domestic/">Domestic（日本語・査読）</a> ｜ 
  <a href="/publications/conferences/">Conferences</a>
</p>
<hr/>

<div class="entries-list">
{% assign pubs = site.publications | sort: "date" | reverse %}
{% for post in pubs %}
  {% include archive-single.html %}
{% endfor %}
</div>
