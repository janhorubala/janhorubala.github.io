---
layout: page
title: Music
permalink: /music/
---

<div class="posts">
  {% for post in site.music %}
      <a class="song-link" href="{{ site.baseurl }}{{ post.url }}">{{ post.title }} {%if post.text %} - {{post.text}} {% endif %}</a>
  {% endfor %}
</div>

<br>
<div class="song-hr"></div>

<h2>Concerts</h2>
<div class="posts">
  {% for post in site.concerts reversed %}
      <a class="song-link" href="{{ site.baseurl }}{{ post.url }}">{{ post.title }} - {{ post.date | date: "%B %e, %Y" }}</a>
  {% endfor %}
</div>

<br>
<div class="song-hr"></div>

<h2>Photos & Graphics</h2>

