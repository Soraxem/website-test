---
layout: default
title: Home
---
# Hello World!

This is my personal website, here a huge part of my knowledge base is published. As well as some highlights.


{%- assign paths = site.pages | map: "path" -%}

{%- assign dir = paths.first | split: "/" | first | prepend: "~" -%}
{%- assign dirs = "" -%}

<ul>
{%- for path in paths -%}
	{%- assign pat = path | prepend: "~" -%}
	{%- if pat contains "~" -%}
		{%- assign dir = pat | split: "/" | first -%}
		{%- assign dirs_array = dirs | split: "~" -%}
		{%- assign dirs_array_uniq = dirs | append: dir | split: "~" | uniq -%}
		{%- unless dirs_array == dirs_array_uniq -%}
			{% assign dirs = dirs | append: dir -%}
			<li href="{{ path }}">{{ dir }}</li>
		{%- endunless -%}		
 	{%- endif -%}
{%- endfor -%}
</ul>
