---
layout: post
title: "standard blog style post"
date: 2017-03-06 09:38:02
categories: jekyll update
---

this is test to standard blog style
<ul>
	{% for post in site.posts %}
		<li>
			<a herf = "{{ post.url }}">{{ post.title }}</a>
		</li>
	{% endfor %}
</ul>
