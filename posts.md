---
layout: page
title: Archives 
permalink: /posts/
cover: false
sitemap:
  lastmod: 2014-01-23
  priority: 0.7
  changefreq: 'monthly'
  exclude: 'yes'
---
### Posts

{% for post in site.posts %}
  * {{ post.date | date_to_string }}:  [ {{ post.title }} ]({{ post.url }})
{% endfor %}

### Projects

{% assign projectList = (site.pages | where: "type" , "project" | sort: 'title') %}
{% for p in projectList %}[ {{ p.title }} ]({{ p.url }}){% if forloop.last == true %}.{% else %},{% endif %}{% endfor %}


