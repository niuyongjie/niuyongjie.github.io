---
layout: post
title: "standard blog style post"
date: 2017-03-06 09:38:02
tag: tag1 ;tag2
---

this is test to standard blog style

<ul>

{% for member in site.data.members %}
<li><a href = "https://github.com/{{ memeber.github }}">
	{{ memeber.name}}
</a></li>
{% endfor %}
</ul>
