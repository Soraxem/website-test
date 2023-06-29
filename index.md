---
layout: default
title: Home
---
# Hello World!

This is my personal website, here a huge part of my knowledge base is published. As well as some highlights.

{% for page in site.pages %}
  {{ page.path }}
  {% assign path_array = page.path | split: "/" %}
  <ul>
  {% for dir in path_array %}
    <li>{{ dir }}</li>
  {% endfor %}
  </ul>
{% endfor %}

{% assign level = site.pages | map: "path" -%}
<ul>
  {% for path in level -%}
    <li>{{ path }}</li>
  {% endfor -%}
</ul>

{% assign paths = site.pages | map: "path" -%}
{% assign step = path | split: "/" -%}
{% assign step = level.first %}
{% for path in paths -%}
  {% assign step = path | split: "/" %}
  {% assign level = level | append: ";" | append: step.first -%}
{% endfor -%}
{{ level }}
