---
layout: page
title: Tags
permalink: /tags/
---

# Tags

{% assign all_tags = "" | split: "" %}
{% for post in site.posts %}
  {% for tag in post.tags %}
    {% assign all_tags = all_tags | push: tag %}
  {% endfor %}
{% endfor %}
{% assign sorted_tags = all_tags | uniq | sort %}

<ul class="tag-list">
{% for tag in sorted_tags %}
  {% assign tag_posts = site.posts | where_exp: "post", "post.tags contains tag" %}
  <li><a href="{{ '/tags/' | append: tag | slugify | relative_url }}/">{{ tag | upcase }}</a> ({{ tag_posts.size }})</li>
{% endfor %}
</ul>
