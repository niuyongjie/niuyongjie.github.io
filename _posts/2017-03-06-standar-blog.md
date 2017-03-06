---
layout: post
title: "standard blog style post"
date: 2017-03-06 09:38:02
author: dave
---

this is test to standard blog style

{% assign author = site.data.people[page.author] %}

<a rel = "author"
   href = "https://twitter.com/{{author.twitter}}"
   title = "{{author.name}}">
	{{author.name}}
</a>
