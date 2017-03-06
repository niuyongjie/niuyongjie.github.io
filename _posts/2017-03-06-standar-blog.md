---
layout: post
title: "standard blog style post"
date: 2017-03-06 09:38:02
tag: tag1 ;tag2
---

this is test to standard blog style
<ul>
	{% for post in site.posts %}
			<a herf = "{{post.url }}">{{ post.title }}</a>
	{% endfor %}
</ul>

{{paginator.per_page}}
total_posts:{{paginator.total_posts}}
total_pages:{{paginator.total_pages}}
page:{{paginator.page}}
next_page:{{paginator.next_page}}
