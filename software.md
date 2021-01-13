---
title: Software
order: 20
---

{% assign pages_list = site.software | sort:"date" | reverse %}

{% for post in pages_list %}
<div class="katalog">
      <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
      <p class="datum">{{ post.date | date_to_string }}</p>
      {{ post.excerpt }}
      <p class="cele"><a href="{{ post.url }}">[Více →]</a></p>
</div>
{% endfor %}
