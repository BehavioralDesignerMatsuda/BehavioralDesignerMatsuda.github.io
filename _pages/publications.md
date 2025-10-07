---
title: "Publications｜論文"
permalink: /publications/
layout: single
author_profile: true
---

<!-- Publications toggle (ALL | Journals | Domestic | Conferences) -->
<div class="pub-filter-wrap">
  <div class="pub-tabs" role="tablist" aria-label="Publications filter" id="pub-tabs">
    <button class="pub-tab" role="tab" aria-selected="true" data-filter="all" id="tab-all">
      ALL <span class="pub-count" data-count-for="all"></span>
    </button>
    <button class="pub-tab" role="tab" aria-selected="false" data-filter="journals" id="tab-journals">
      Journals（英語・査読）<span class="pub-count" data-count-for="journals"></span>
    </button>
    <button class="pub-tab" role="tab" aria-selected="false" data-filter="domestic" id="tab-domestic">
      Domestic（日本語・査読）<span class="pub-count" data-count-for="domestic"></span>
    </button>
    <button class="pub-tab" role="tab" aria-selected="false" data-filter="conferences" id="tab-conferences">
      Conferences <span class="pub-count" data-count-for="conferences"></span>
    </button>
  </div>
</div>

<noscript>
  <p>
    <a href="/publications/journals/">Journals（英語・査読）</a> ｜ 
    <a href="/publications/domestic/">Domestic（日本語・査読）</a> ｜ 
    <a href="/publications/conferences/">Conferences</a>
  </p>
</noscript>

<hr/>

<div class="entries-list">
{% assign pubs = site.publications | sort: "date" | reverse %}
{% for post in pubs %}
  {% include archive-single.html %}
{% endfor %}
</div>
