---
layout: page
published: true
title: Metasploit
type: page
---

Metasploit
==========

{% for module in site.data.modules %}
* [{{ module.name }}](https://www.rapid7.com/db/modules/{{ module.name }})  
  {{ module.description }}
{% endfor %}
