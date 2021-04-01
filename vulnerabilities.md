---
layout: page
published: true
title: Vulnerabilities
type: page
---

Vulnerabilities
===============

{% for vulnerability in site.data.vulnerabilities %}
* [{{ vulnerability.name }}](https://cve.mitre.org/cgi-bin/cvename.cgi?name={{ vulnerability.name }})  
  {{ vulnerability.description }}
{% endfor %}
