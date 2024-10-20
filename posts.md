---
layout: home.njk
title: Posts
---

# Take a look at all my posts 👀

<ul>
{% for post in collections.posts %}
  <li>
    <a href="{{ post.url }}">{{ post.data.title }}</a>
  </li>
{% endfor %}
</ul>

