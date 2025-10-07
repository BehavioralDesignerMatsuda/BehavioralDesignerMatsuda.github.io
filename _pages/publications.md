---
title: "Publications｜論文"
permalink: /publications/
layout: single
author_profile: true
---

<!-- ▼ トグルUI（ALL / Journals / Domestic / Conferences） -->
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

<!-- ▼ 一覧本体（各アイテムに data-kind を付与して自前描画） -->
<div class="entries-list" id="pub-list">
{% assign pubs = site.publications | sort: "date" | reverse %}
{% for item in pubs %}

  {% comment %}
    kind を front matter から頑健に推定：
    - categories（配列）があれば join → 文字列検索
    - なければ category（文字列）を検索
  {% endcomment %}
  {% if item.categories %}
    {% assign cats_joined = item.categories | join: ' ' | downcase %}
  {% elsif item.category %}
    {% assign cats_joined = item.category | downcase %}
  {% else %}
    {% assign cats_joined = '' %}
  {% endif %}

  {% assign kind = 'other' %}
  {% if cats_joined contains 'journal' %}
    {% assign kind = 'journals' %}
  {% elsif cats_joined contains 'domestic' or cats_joined contains 'japanese' %}
    {% assign kind = 'domestic' %}
  {% elsif cats_joined contains 'conference' %}
    {% assign kind = 'conferences' %}
  {% endif %}

  <article class="archive__item pub-item" data-kind="{{ kind }}" itemscope itemtype="http://schema.org/CreativeWork">
    <h3 class="archive__item-title" itemprop="headline">
      <a href="{{ item.url | relative_url }}" rel="permalink">{{ item.title }}</a>
    </h3>

    {%- comment -%} 著者表示（authors / author / citation）+ 自分の名前を太字 {%- endcomment -%}
    {% assign authors_line = nil %}
    {% if item.authors %}
      {% assign authors_line = item.authors | join: ", " %}
    {% elsif item.author %}
      {% assign authors_line = item.author %}
    {% elsif item.citation %}
      {%- assign authors_line = item.citation | split: '(' | first | strip -%}
    {% endif %}

    {%- comment -%} ご本人名（英/日/表記揺れ）を太字に置換 {%- endcomment -%}
    {% if authors_line %}
      {% assign my_en = "Soichiro Matsuda" %}
      {% assign my_en_rev = "Matsuda Soichiro" %}
      {% assign my_ja = "松田 壮一郎" %}
      {% assign my_ja_nospace = "松田壮一郎" %}
      {% assign authors_line = authors_line
        | replace: my_en, "<strong>Soichiro Matsuda</strong>"
        | replace: my_en_rev, "<strong>Matsuda Soichiro</strong>"
        | replace: my_ja, "<strong>松田 壮一郎</strong>"
        | replace: my_ja_nospace, "<strong>松田壮一郎</strong>" %}
      <p class="archive__item-authors">{{ authors_line }}</p>
    {% endif %}

    {% assign year = item.date | date: "%Y" %}
    <div class="archive__item-meta">
      <span>{{ year }}</span>
      {% if item.venue %}<span> · {{ item.venue }}</span>{% endif %}
      {% if kind != 'other' %}<span> · {{ kind | capitalize }}</span>{% endif %}
    </div>

    {% if item.excerpt or item.description %}
      <p class="archive__item-excerpt" itemprop="description">
        {{ item.excerpt | default: item.description | markdownify | strip_html }}
      </p>
    {% endif %}
  </article>

{% endfor %}
</div>

<!-- ▼ フィルタ用スクリプト（URLハッシュ保持／件数バッジ／キーボード対応） -->
<script>
(function(){
  const TABS = document.querySelectorAll('#pub-tabs .pub-tab');
  const LIST = document.querySelector('#pub-list');
  const ITEMS = LIST ? Array.from(LIST.querySelectorAll('.pub-item')) : [];

  function setSelected(tab) {
    TABS.forEach(b => b.setAttribute('aria-selected', String(b === tab)));
  }

  function applyFilter(filter) {
    const f = (filter||'all').toLowerCase();
    ITEMS.forEach(el => {
      const kind = (el.getAttribute('data-kind')||'').toLowerCase();
      const show = (f === 'all') || (kind === f);
      if (show) {
        el.removeAttribute('hidden');
        el.style.opacity = '1';
        el.style.transform = 'translateY(0)';
      } else {
        el.setAttribute('hidden', '');
      }
    });
    const newHash = '#pubtab=' + encodeURIComponent(f);
    if (history.replaceState) history.replaceState(null, '', newHash);
    updateCounts();
  }

  function updateCounts() {
    const counters = document.querySelectorAll('[data-count-for]');
    const counts = { all: ITEMS.length, journals: 0, domestic: 0, conferences: 0 };
    ITEMS.forEach(el => {
      const k = (el.getAttribute('data-kind')||'').toLowerCase();
      if (counts.hasOwnProperty(k)) counts[k]++;
    });
    counters.forEach(c => {
      const key = c.getAttribute('data-count-for');
      const n = counts[key] != null ? counts[key] : 0;
      c.textContent = n ? ` (${n})` : '';
    });
  }

  function parseInitialFilter() {
    const m = (location.hash || '').match(/pubtab=([^&]+)/i);
    return m ? decodeURIComponent(m[1]) : 'all';
  }

  function focusNext(current, dir) {
    const arr = Array.from(TABS);
    const i = arr.indexOf(current);
    const j = (i + dir + arr.length) % arr.length;
    arr[j].focus();
  }

  if (!TABS.length || !ITEMS.length) return;
  updateCounts();

  const initial = parseInitialFilter();
  const initialTab = Array.from(TABS).find(b => (b.dataset.filter||'') === initial) || TABS[0];
  setSelected(initialTab);
  applyFilter(initial);

  TABS.forEach(btn => {
    btn.addEventListener('click', () => {
      setSelected(btn);
      applyFilter(btn.dataset.filter);
    });
    btn.addEventListener('keydown', (e) => {
      if (e.key === 'ArrowRight') { e.preventDefault(); focusNext(btn, +1); }
      else if (e.key === 'ArrowLeft') { e.preventDefault(); focusNext(btn, -1); }
      else if (e.key === 'Home') { e.preventDefault(); TABS[0].focus(); }
      else if (e.key === 'End') { e.preventDefault(); TABS[TABS.length-1].focus(); }
    });
  });

  window.addEventListener('hashchange', () => {
    const f = parseInitialFilter();
    const tab = Array.from(TABS).find(b => (b.dataset.filter||'') === f);
    if (tab) { setSelected(tab); applyFilter(f); }
  });
})();
</script>
