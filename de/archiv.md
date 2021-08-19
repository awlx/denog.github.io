---
title: Archiv
lang: de
ref: archiv
---
# Slides

Slides vergangener Veranstaltungen finden sich im [Media Repository](https://github.com/denog/media)

{% assign meetingArray = site.pages|where: "lang", page.lang | sort: 'year' %}
{% assign searchString = page.lang|append: '/meetings/denog'|prepend: '/' %}
{% assign currentYear = site.time|date: '%Y'|plus: 0 %}
{% assign presentations = site.static_files | where: "media", true %}

{% for entry in meetingArray reversed %}
    {% if entry.url contains searchString %}
        {% if entry.home and entry.home == true %}
            {% assign checkYear = entry.year|plus: 0 %}
            {% if checkYear < currentYear and checkYear > 0 %}
**{{ entry.year }} {{ entry.meeting }} Meeting**\\
[{{ entry.meeting }}, {{ entry.city }}]({{ entry.url }})\\
**Slides:**
                {% for presentation in presentations %}
                    {% if presentation.path contains entry.meeting %}
- [{{ presentation.basename | replace: "_", " " }}]({{ presentation.path }})
                    {% endif %}
                {% endfor %}
            {% endif %}
        {% endif %}
    {% endif %}
{% endfor %}