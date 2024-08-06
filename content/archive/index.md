---
layout: layouts/base.njk
eleventyNavigation:
  key: Site Map
  order: 5
---
# Site Map.

If you're lost, you can [go back home](/) or browse pages and categories below!

<h2>All pages</h2>

{% macro listLevels(listOfPages) %}
	{% for linkPage in listOfPages %}
		{% if loop.first %}<ol {% if linkPage.parentKey == "Blog" %}start=0 {% endif %}>{% endif %}
			<li>
				<a
					href="{{ linkPage.url }}"
					{% if linkPage.docLang != lang %}
						hreflang="{{ linkPage.docLang }}"
						lang="{{ linkPage.docLang }}"
					{% endif %}
					{% if linkPage.url == page.url %}
						aria-current=page
					{% endif %}
				>{{ linkPage.title }}{% if linkPage.docLang != lang %} ({{ linkPage.docLang }}){% endif %}</a>
				{{ listLevels(linkPage.children) }}
			</li>
		{% if loop.last %}</ol>{% endif %}
	{% endfor %}
{% endmacro %}

<main>
{% include "breadcrumb.njk" %}
<h1>{{ title | failIfMissing }}</h1>

{% set navPages = collections.all | eleventyNavigation %}
{{ listLevels(navPages) }}

</main>

<h1>All tags</h1>

<ul>
{% for tag in collections.all | getAllTags | filterTagList %}
	{% set tagUrl %}/tags/{{ tag | slugify }}/{% endset %}
	<li><a href="{{ tagUrl }}" class="post-tag">{{ tag }}</a></li>
{% endfor %}
</ul>
