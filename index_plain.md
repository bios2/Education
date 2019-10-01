---
title: BIOS2 lessons
layout: index
---

# BIOS2 Data Management Education Modules

{% comment %}
The following part extracts all the tags from the lessons
{% endcomment %}
{% assign rawtags = "" %}
{% assign rawcats = "" %}
{% for lesson in site.lessons %}
	{% assign ttags = lesson.tags | join:'|' | append:'|' %}
	{% assign rawtags = rawtags | append:ttags %}
	{% assign ccats = lesson.categories | join:'|' | append:'|' %}
	{% assign rawcats = rawcats | append:ccats %}
{% endfor %}
{% assign rawtags = rawtags | split:'|' | sort %}
{% assign rawcats = rawcats | split:'|' | sort %}

{% comment %}
Removes duplicated tags
{% endcomment %}
{% assign tags = "" %}
{% for tag in rawtags %}
	{% if tag != "" %}
		{% if tags == "" %}
			{% assign tags = tag | split:'|' %}
		{% endif %}
		{% unless tags contains tag %}
			{% assign tags = tags | join:'|' | append:'|' | append:tag | split:'|' %}
		{% endunless %}
	{% endif %}
{% endfor %}
{% assign cats = "" %}
{% for cat in rawcats %}
	{% if cat != "" %}
		{% if cats == "" %}
			{% assign cats = cat | split:'|' %}
		{% endif %}
		{% unless cats contains cat %}
			{% assign cats = cats | join:'|' | append:'|' | append:cat | split:'|' %}
		{% endunless %}
	{% endif %}
{% endfor %}

{% comment %}
Show the tags which are now in the tags list.
{% endcomment %}

## Tags
```
{% for tag in tags %}
* [{{ tag }}](#{{ tag | slugify }}){% endfor %}
```

## Categories
```
{% for cat in cats %}
* [{{ cat }}](#{{ cat | slugify }}){% endfor %}
```

## Lessons
```
{% for lesson in site.lessons %}
  {{ lesson.url }}
  {{ lesson.keys | jsonify }}
{% endfor %}
```
{% assign idx = 0 %}
{% for lesson in site.lessons %}
  {% assign ldeck = lesson.url | split: '/' %}
  {% assign ldeck = ldeck[2] %}
- {{ ldeck }} [![{{ lesson.title }}]({{ site.baseurl }}/lessons/{{ ldeck }}/{{ ldeck }}.png)]({{ site.baseurl }}{{ lesson.url }}) [PDF]({{ site.baseurl }}/lessons/{{ ldeck }}/{{ ldeck }}.pdf)
  - {{ lesson.categories | join: ',' | replace: ' ','_' }}
{% endfor %}
