---
title: ""
---

<div class="bodystr">

{% assign pages_list = site.software | sort:"date" | reverse %}

{% for post in pages_list limit:5 %}
<div class="katalog">
      <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
      <p class="datum">{{ post.date | date_to_string }}</p>
      {{ post.excerpt | replace: "h2", "h4" }}
      <p class="cele"><a href="{{ post.url }}">[Více →]</a></p>
</div>
{% endfor %}
</div>