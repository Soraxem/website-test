---
layout: default
title: Home
---
# Hello World!

This is my personal website, here a huge part of my knowledge base is published. As well as some highlights.


<ul>
  {% assign root = site.pages | where: "path", "/" | first %}
  {% assign topLevelPages = site.pages | where: "dir", root.dir | sort: "path" %}
  {% for page in topLevelPages %}
    <li>
      <a href="{{ site.baseurl }}{{ page.url }}">{{ page.url | remove: "/" }}</a>
      {% assign childPages = site.pages | where: "dir", page.dir | sort: "path" %}
      {% if childPages.size > 0 %}
        <ul>
          {% for childPage in childPages %}
            {% unless childPage.url == page.url %}
              <li><a href="{{ site.baseurl }}{{ childPage.url }}">{{ childPage.url | remove: "/" }}</a></li>
            {% endunless %}
          {% endfor %}
        </ul>
      {% endif %}
    </li>
  {% endfor %}
</ul>

{% assign root = site.pages | where: "path", "/" | first %}
{% assign topLevelPages = site.pages | where_exp: "page", "page.path != '/'" | sort: "path" %}

<ul>
  {% for page in topLevelPages %}
    {% assign pageName = page.path | split: "/" | last %}
    <li>
      <a href="{{ site.baseurl }}{{ page.url }}">{{ pageName }}</a>
      {% assign childPages = site.pages | where_exp: "childPage", "childPage.url != page.url" | where_exp: "childPage", "childPage.path contains page.path" | sort: "path" %}
      {% if childPages.size > 0 %}
        <ul>
          {% for childPage in childPages %}
            {% assign childPageName = childPage.path | split: "/" | last %}
            <li><a href="{{ site.baseurl }}{{ childPage.url }}">{{ childPageName }}</a></li>
          {% endfor %}
        </ul>
      {% endif %}
    </li>
  {% endfor %}
</ul>

{% assign root = site.pages | where: "path", "/" | first %}
{% assign topLevelPages = site.pages | where_exp: "page", "page.path != '/'" | sort: "path" %}

<ul>
  {% for page in topLevelPages %}
    {% assign pageName = page.path | split: "/" | last %}
    {% assign pageDepth = page.path | split: "/" | size | minus: 1 %}
    <li>
      <a href="{{ site.baseurl }}{{ page.url }}">{{ pageName }}</a>
      {% assign childPages = site.pages | where_exp: "childPage", "childPage.url != page.url" | where_exp: "childPage", "childPage.path contains page.path" | sort: "path" %}
      {% if childPages.size > 0 %}
        {% assign childDepth = pageDepth | plus: 1 %}
        {% include recursive_navigation.html pages=childPages depth=childDepth %}
      {% endif %}
    </li>
  {% endfor %}
</ul>

{% assign root = site.pages | where: "path", "/" | first %}
{% assign topLevelPages = site.pages | where_exp: "page", "page.path != '/'" | sort: "path" %}

<ul>
  {% for page in topLevelPages %}
    {% assign pageName = page.path | split: "/" | last %}
    <li>
      <a href="{{ site.baseurl }}{{ page.url }}">{{ pageName }}</a>
      {% assign childPages = site.pages | where_exp: "childPage", "childPage.url != page.url" | where_exp: "childPage", "childPage.path contains page.path" | sort: "path" %}
      {% if childPages.size > 0 %}
        {% include recursive_navigation.html pages=childPages parent=page %}
      {% endif %}
    </li>
  {% endfor %}
</ul>

{% assign root = site.pages | where: "path", "/" | first %}
{% assign topLevelPages = site.pages | where_exp: "page", "page.path != '/'" | sort: "path" %}

<ul>
  {% for page in topLevelPages %}
    {% assign pageName = page.path | split: "/" | last %}
    <li>
      <a href="{{ site.baseurl }}{{ page.url }}">{{ pageName }}</a>
      {% assign childPages = site.pages | where_exp: "childPage", "childPage.url != page.url" | where_exp: "childPage", "childPage.path contains page.path" | sort: "path" %}
      {% if childPages.size > 0 %}
        {% include recursive_navigation.html pages=childPages parent=page %}
      {% endif %}
    </li>
  {% endfor %}
</ul>

{% for page in site.pages %}
  {{ page.path }}
  {% assign path_array = page.path | split: "/" %}
  <ul>
  {% for dir in path_array %}
    <li>{{ dir }}</li>
  {% endfor %}
  </ul>
{% endfor %}
