---
layout: archive
title: "All Archives"
permalink: /archive-preview/
author_profile: true
---
<!-- Popular Tags -->
<h2 class="archive__item-title">Populars Tags</h2>
<ul class="taxonomy__index">
  {% assign tags_max = 0 %}
  {% for tag in site.tags %}
    {% if tag[1].size > tags_max %}
      {% assign tags_max = tag[1].size %}
    {% endif %}
  {% endfor %}
  {% assign count = 0 %}
  {% for i in (1..tags_max) reversed %}
    {% for tag in site.tags %}
      {% if tag[1].size == i %}
        <li>
          <a href="/tags/#{{ tag[0] | slugify }}">
            <strong>{{ tag[0] }}</strong> <span class="taxonomy__count">{{ i }}</span>
          </a>
        </li>
        {% assign count = count | plus: 1 %}
      {% endif %}
      {% if count == 9 %}{% break %}{% endif %}
    {% endfor %}
    {% if count == 9 %}{% break %}{% endif %}
  {% endfor %}
</ul>
<h2 class="back-to-top">
<a href="/tags/">View All Tags</a>
</h2>

<!-- Popular Categories -->
<h2 class="archive__item-title">Populars Categories</h2>
<ul class="taxonomy__index">
  {% assign categories_max = 0 %}
  {% for category in site.categories %}
    {% if category[1].size > categories_max %}
      {% assign categories_max = category[1].size %}
    {% endif %}
  {% endfor %}
  {% assign count = 0 %}
  {% for i in (1..categories_max) reversed %}
    {% for category in site.categories %}
      {% if category[1].size == i %}
        <li>
          <a href="/categories/#{{ category[0] | slugify }}">
            <strong>{{ category[0] }}</strong> <span class="taxonomy__count">{{ i }}</span>
          </a>
        </li>
        {% assign count = count | plus: 1 %}
      {% endif %}
      {% if val == 9 %}{% break %}{% endif %}
    {% endfor %}
    {% if val == 9 %}{% break %}{% endif %}
  {% endfor %}
</ul>
<h2 class="back-to-top">
<a href="/categories/">View All Categories</a>
</h2>

<!-- Popular Years -->
<h2 class="archive__item-title">Populars Years</h2>
<ul class="taxonomy__index">
  {% assign postsInYear = site.posts | group_by_exp: 'post', 'post.date | date: "%Y"' | limit:6 %}
  {% for year in postsInYear %}
    <li>
      <a href="/year-archive/#{{ year.name }}">
        <strong>{{ year.name }}</strong> <span class="taxonomy__count">{{ year.items | size }}</span>
      </a>
    </li>
  {% endfor %}
</ul>
<h2 class="back-to-top">
<a href="/year-archive/">View All Years</a>
</h2>
