---
layout: default
---

# My Projects

<div class="projects">
  {% for post in site.projects %}
   	<div class="pro-tab">
	   	<div class="pro-cover" style="background-image: url({{ site.baseurl }}{{ post.cover }})">
	   	</div>
	   	<div class="pro-title">{{ post.title }}</div>
	   	<a class="pro-btn" href="{{ site.baseurl }}{{ post.url }}">Read</a>
	   	<a class="pro-btn" href="{{ post.webpage }}" target="_blank">View</a>
   </div>
  {% endfor %}
</div>

<!-- 
			<div class="pro-info">
		    <h1><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h1>
	      {{ post.description }}
      </div>
 -->