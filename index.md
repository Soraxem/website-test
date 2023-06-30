---
layout: default
title: Home
---
# Hello World!

This is my personal website, here a huge part of my knowledge base is published. As well as some highlights.

```liquid

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

{% assign dir = paths.first | split: "/" | first | prepend: "~" -%}
{% assign dirs = "" -%}

{% for path in paths -%}
	{% assign pat = path | prepend: "~" -%}
	{% if pat contains "~" -%}
 		{% assign dir = pat | split: "/" | first %}

		{% assign dirs_array = dirs | split: "~" -%}
  		{% assign dirs_array_uniq = dirs | append: dir | split: "~" | uniq -%}

		<ul>
 		{% unless dirs_array == dirs_array_uniq -%}
	 		{% assign dirs = dirs | append: dir -%}
			<li>{{ dir }}</li>
    		{% endunless -%}
		</ul>
 	{% endif -%}
{% endfor -%}

```
