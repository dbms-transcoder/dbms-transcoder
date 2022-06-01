---
layout: default
title: Authors
---
All authors on this project:

{% for person in site.people %}

* <a href="{{ site.baseurl }}{{ person.url }}">{{ person.name }}</a>

{% endfor %}
