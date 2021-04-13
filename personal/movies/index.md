---
layout: default
date: 2021-02-22
author: Jason Brown
title: Movies
---
Here I'll list my favorite movies separated by genre in no particular order, as well as a few other lists like my least favorite. I plan to write down my thoughts and explain my reasons for liking or disliking each particular movie and will link to those from here.

{% assign tags = site.movies | map: "tags" | join: "," | split: "," | uniq %}
{% for tag in tags %}
## {{ tag }}
	{% for movie in site.movies %}
		{% if movie.tags contains tag %}
			{% assign content = movie.content | strip_newlines %}
			{% if content != "" %}
* [{{ movie.title }} ({{ movie.release-year }})]({{ movie.url }}) - *{{ movie.director }}*
			{% else %}
* {{ movie.title }} ({{ movie.release-year }}) - *{{ movie.director }}*
			{% endif %}
		{% endif %}
	{% endfor %}
{% endfor %}
