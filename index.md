---
layout:default
title:我的Blog
---

## {{ page.title }}

博客搭建测试:

<ul>
	{% for post in site.posts %}
	<li>
		{{ post.date | date_to_string }} <a href="{{ site.baseurl }}{{ post.url }}"></a>
	</li>
	{% endfor %}
</ul>
