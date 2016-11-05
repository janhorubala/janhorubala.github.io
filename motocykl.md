---
layout: page
title: Motocykl
permalink: /motocykl/
---

Notatki z kursu na kategorię A prowdzonego przez Tomka Kulika w szkole <a href='http://www.kulikowisko.pl/' target='_blank'>kulikowisko.pl</a>


<div class="posts">
  {% for post in site.motocykl %}
    <article class="post">

      <h1><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h1>

      <div class="entry">
        {{ post.excerpt }}
      </div>

      <a href="{{ site.baseurl }}{{ post.url }}" class="read-more">Read More</a>
    </article>
  {% endfor %}
</div>